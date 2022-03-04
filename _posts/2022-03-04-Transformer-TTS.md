---
layout: post
title: Transformer-TTS
date: 2022-03-03 00:10:00 +0900
category: ongoing
use_math: true
comments: true
---

본 포스팅은 아래 논문을 참고했습니다.

- <https://arxiv.org/pdf/1809.08895.pdf>
- <https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=sooftware&logNo=221661644808>

---

## Abstract

- 기존의 end-to-end TTS 방법(Tacotron2)은 두가지 문제가 있었다.
  - 학습과 추론 시 낮은 효율성
  - RNN으로는 long dependency를 modeling 하기 어려움
- transformer
  - multi-head self-attention으로 hidden state가 parallel해졌고, 학습 효율성을 향상시켰다.
  - self-attention : long range dependency 문제를 해소
- 음소 시퀀스를 넣으면 WaveNet vocoder로부터 나오는 mel spectrogram으로 출력
- 효율성과 성능을 중심으로 테스트 하였다.
  - Tacotron2보다 4.25배 학습 속도가 빨랐다.
  - Tacotron2보다 성능도 좋았다.

    <details>
    <summary>
        MFCC, Mel-Spectrogram
    </summary>
    <div markdown="1">
    - '음성데이터'를 '특징벡터' (Feature) 화 해주는 알고리즘
    - MFCC Feature는 파이썬에서는 제공되는 librosa라는 라이브러리를 이용해서 간단하게 뽑아올 수 있다.
    - Mel-scale : 사람의 달팽이관 특성 고려, 저주파 대역은 잘 감지, 고주파 대역은 감지 어려움
    - 아래와 같이 사용
    ![alt text](/public/img/220303/mfcc.png)
    </div>
    </details>
---

## 1. Introduction

### TTS의 흐름

1. Traditional TTS system은 front-end와 back-end가 있었다.
   - front-end는 text 분석, 언어적 특징 추출
   - back-end는 음성 합성
   - 이런 방법은 복잡하고, 시간도 많이 걸렸고, 성능도 좋지 않았다.
2. end-to-end generative tts model
    - Tacotron, Tacotron2
    - mel spectogram을 text로 부터 추출
    - vocoder로 음성 생성(Griffin Lim algorithm, WaveNet)
    - encoder랑 decoder로 구성
    - encoder : semantic space에 input sequence를 mapping, generate sequence
    - decoder : contest information을 받아서 mel frames를 출력
3. RNN은 sequentially 하게 동작하기 때문에 예전의 많은 step이 biased 된다.
4. Transformer로 long distance dependency 문제를 해소
5. Transformer TTS는 mel spectrogram을 합성하고, wavenet을 vocoder로 audio를 합성한다.

---

## 2. Background

---

## 3. Neural TTS with Transformer

---

## 4. Experience

---

## 5. Related work

---

## 6. Conclusion and Future work
