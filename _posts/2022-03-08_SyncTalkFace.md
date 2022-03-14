---
layout: post
title: SyncTalkFace
date: 2022-03-08 00:10:00 +0900
category: deep-learning
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
   4. Audio를 향상시킨 방법 : Audio를 phonetic content, emotional tone 등으로 나눠서 Variational Autoencoder를 사용하고, negative log likelihood와 margin ranking loss를 사용하였다.
   5. 
2. intermediate representation based method

---

## 3. Methods

---

## 4. Experiment

---

## 5. Conclusion