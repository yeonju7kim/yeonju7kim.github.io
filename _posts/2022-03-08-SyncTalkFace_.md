---
layout: post
title: SyncTalkFace
date: 2022-03-08 00:10:00 +0900
# category: ongoing
category: lab-paper
use_math: true
comments: true
---

본 포스팅은 아래 게시물을 참고했습니다.

- <https://www.aaai.org/AAAI22Papers/AAAI-7528.ParkS.pdf>

---

연구실의 논문을 읽어보았습니다.

## Abstract

- 말하는 얼굴 합성에는 audio와 video의 싱크 맞추는 것이 어렵다.
- 기존에는 소리와 입모양을 학습하거나 다른 구조적인 정보를 사용하는 방법을 사용했다. 하지만 한계가 있었다.
- 이 논문에서는 audio-lip memory를 사용하였다.
  - Memory에는 GT image에서 lip motion feature를 value로 저장
  - audio input을 통해 lip motion feature을 꺼냄
- memory 분석을 통해 각 memory slot에 음소 레벨로 각각 다른 lip feature가 저장되는 것을 확인했다.
- lip-syncing performance 를 높이기 위해 visual-visual synchronization loss를 사용했다.

---

## 1. Introduction

- lip-sync에서는 audio와 시각정보의 정렬을 맞추는 것이 어려움
- 기존의 encoder-decoder 구조 : 불필요한 정보를 제거하기 위해 feature 나누기에 집중
  - metric learning 방법으로 visual input을 identity와 speech content space로 나누고, visual feature간의 공유하는 latent space에 임베딩하여 audio를 향상시켰다.
  - audio 표현을 phonetic content, emotional tone 등으로 나누었다.
  - 나눠진 audio 표현은 visual 정보를 담기에 충분하지 않다.
- 최근 연구 : facial landmark와 3D model과 같은 intermediate structural representation을 사용
  - facial landmark은 lip-synchronization을 하기에 부족하고, 3D model은 정밀한 detail을 포착하기 어렵다.
  - generation network와 별도로 intermediate representation을 얻는 것에 한계가 있었다.
- 이 논문
  - memory에 audio와 lip feature를 연결하여 저장하고, audio를 query로 사용함.
  - memory로 얻은 lip feature, audio feature은 decoder로 들어가서 talking face video를 합성한다.
  - decoder가 memory로 얻은 명확한 visual hint를 사용하게 된다.

  > 1. audio와 lip-movement intermediate representation을 연결하는 Audio-Lip Memory 사용
  > 2. 높은 audio-visual sync를 보장한다.
  > 3. representation이 memory 안에서 phoneme level로 저장되는 것을 확인했다.
  > 4. LRW, LRS2 dataset에서 sota 성능

---

## 2. Related work

### Talking face generation

1. reconstruction based method
   1. encoder-decoder 구조를 따른다. 여기서 identity feature와 speech feature이 추출되고, 둘이 결합돼서 decoder의 input으로 들어간다. 그리고 talking face video를 합성한다.
   2. pretrained된 lip-sync discriminator를 사용한 방법 : 정확한 lip-sync discriminator의 중요성을 강조했다. 여기서 lip-sync discriminator는 lip-sync 성능을 network에 피드백한다.
   3. visual input을 identity space, pose space, speech content space로 나누는 방법 : 많은 비슷한 이전 작업들이 이렇게 visual representation을 향상시켰지만 audio representation을 향상시키지는 못했다.
   4. Audio를 향상시킨 방법 : Audio를 phonetic content, emotional tone 등으로 나눠서 negative log likelihood와 KL divergence로 Variational Autoencoder를 사용하고, margin ranking loss를 사용하였다.
   5. 이 연구에서는 speech를 분해하기보다는 input audio와 연관된 lip motion을 추출했다.
   6. generation 단계에서 lip synchronization을 맞춘다.
2. intermediate representation based method : landmark나 3D 모델과 같은 intermediate representation을 사용하는 방법

### Audio-Visual Alignment

- audio와 video의 상관관계를 찾아서 맞춤.
- pretrained embedding module을 liy-sync discriminator로 사용했고, asymmetric Mutual Information Estimator를 제시했다.
- inter-class pair 뿐만이 아니라 intra-class pair에 대해서도 multi-way matching loss를 사용하는 방법
- 이 논문에서는 intra-class pair loss에서 영감을 받아서 visual-visual sync loss를 이용했다.
- input audio와 ground truth video가 sync가 맞춰지면 audio-visual sync가 맞춰질 것이다.

### Memory Network

- 기존에는 memory에 중요한 정보만 저장했다.
- 이 논문에서는 key-value memory로 2 modality features를 저장한다.
- memory의 value로 얻은 lip feature은 intermediate representation으로 사용되어 audio와 video를 연결한다.

![alt image](/public/img/220315/synctalkface.png)

---

## 3. Methods

- memory에 encoded audio feature과 encoded lip feature을 저장했다. audio feature로 query 했을 때 lip feature을 얻을 수 있다.
- 얻어진 lip feature은 audio feature과 합쳐져서 decoder network로 들어가서 video 합성을 한다.
- sync가 잘 맞는 이유는 audio-visual synchronization loss와 visual-visual synchronization loss를 사용해서이다.

### 3.1 Audio-Lip Memory

- audio key, lip value
- audio encoder로 audio -> spectrogram
- lip encoder로 해당하는 5개의 frame을 입쪽만 보이게 위의 반쪽만 masked하여 GT로 넣음
- memory는 recalled lip feature frome the key address(?)와 lip encoder로 부터 나온 lip features사이의 reconstruction loss로 representative lip feature를 학습한다.
- 동시에 key-value address alignment loss로 lip feature와 audio feature의 align을 학습해서 audio feature로 lip feature를 얻을 수 있도록 학습한다.
  
#### memory에 lip feature를 저장하는 법

- $M_{aud}\in R^{S\times C}$
- $M_{lip}\in R^{S\times C}$
- S : slot 개수, C : channel 수
- 5장의 입쪽만 보이는 GT 이미지와 sound로 합성된 이미지간의 cosine similarity를 계산하여 lip-feature를 학습한다.
  - ![alt image](/public/img/220315/cosine_similarity_synctalkface.png)
- cosine similarity를 계산한 후 softmax를 한다.
  - ![alt image](/public/img/220315/softmax_synctalkface.png)
  - scaling term : $\kappa$
  - lip feature에 대한 i번째 slot의 attention weight : $\alpha$
- memory로부터 lip feature를 아래 식으로 얻는다.
  - ![alt image](/public/img/220316/retrieved_lip_feature.png)
- 아래와 같이 retrieved 된 lip feature와 GT 이미지로 부터 얻은 lip feature로 reconstruction loss를 계산하고, 이것으로 모델이 lip feature을 임베딩 할 수 있게 학습한다.
  - ![alt image](/public/img/220316/memory_loss.png)
  
#### aligning key address with value addresss

- audio가 쿼리로 들어갔을 때, lip-feature를 얻을 수 있게 하는 과정
- memory 안의 audio feature $M_{aud}$와 input으로 들어간 audio feature$f_{aud}$로 코사인 유사도를 이용하여 가중치를 구한다.(lip feature를 메모리에 넣던 것과 비슷하게)
  - ![alt image](/public/img/220316/audio_weight.png)
- key랑 value의 align을 맞추기 위해 key-value address align loss를 아래와 같이 구한다.
  - ![alt image](/public/img/220316/key_value_align_loss.png)
  - KL divergence로 구한다.
    - 두 확률분포의 차이를 계산하는 데 사용하는 함수
    - 이상적인 분포에 대해 그 분포를 근사하는 다른 분포를 사용해 샘플링 하면 발생할 수 있는 정보 엔트로피 차이를 계산한다.
  - key address로 lip feature 구함
    - ![alt image](/public/img/220316/retrieved_lip_feature.png)

### 3.2 video synthesis

- identity encoder가 입쪽이 가려진 target face에서 identity feature를 추출한다.
- recalled lip feature랑 audio feature가 합쳐져서 U-Net-like decoder로 들어간다. 여기서 skip-connection은 input identity와 pose feature을 유지하게 한다.
- training 할 때는 lip encoder로 얻은 lip feature을 추가적으로 사용한다.
- ![alt image](/public/img/220323/recall_lip_feature.png)
  - 위 : train
  - 아래 : test

#### Reconstruction loss

![alt image](/public/img/220323/reconstruction_loss.png)

> generate 된 frame과 gt frame을 비교

#### Generative adversarial loss

![alt image](/public/img/220323/generative_adversarial_loss.png)

> 사실적으로 보이기 위해 추가함.<br>
> 위 : discriminator가 구별 못하도록 loss를 최소화<br>
> 아래 : discriminator를 학습

#### Audio-Visual Sync Loss

![alt image](/public/img/220323/audio_visual_sync_loss.png)

> - audio-visual sync module을 학습
> - audio feature $f_a$와 video feature $f_v$의 코사인 유사도로 binary cross-entropy를 계산하여 loss로 사용한다.

#### Visual-Visual Sync Loss

![alt image](/public/img/220323/visual_visual_sync_loss.png)

> - L1 norm
> - generated frame과 gt frame으로 계산한다.

#### Total Loss

![alt image](/public/img/220323/total_loss.png)

---

## 4. Experiment

### Dataset

- LRW : 1000개 넘는 발화, 500개 이상의 단어
- LRS2 : sentence-level dataset, 140000 발화

### Metrics

- PSNR : visual quality, 최대 신호에서 잡음 비율, 화질에 대한 손실 정보
- SSIM : visual quality, 인간의 시각적 화질 차이를 평가, Luminance, Contrast, Structural 이 3가지 측면에서 품질을 평가
- LMD : lip-sync quality, lip landmarks의 거리 
- LSE-D, LSE-C : lip-sync quality, SyncNet으로 부터 얻은 audio와 video feature 사이의 confidence score과 distance score
- ATVGnet으로 crop해서 평가했다.

![alt image](/public/img/220324/mse.png)

![alt image](/public/img/220324/psnr.png)

![alt image](/public/img/220324/ssim.png)

### Comparison Methods

- SOTA model
  - ATVGnet : attention mechanism으로 생성된 landmark를 조건으로 frame을 생성
  - Wav2Lip : reconstruction-based method
  - PC-AVS : identity, pose, seepch content에 대한 modularized된 audio-visual representation
  - 3D Identity Mem : identity memory로 augment

### Implementation Details

1. 

---

## 5. Conclusion