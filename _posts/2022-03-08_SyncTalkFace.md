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

현재 연구실의 논문을 읽어보았습니다.

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

---

## 2. Related work

---

## 3. Methods

---

## 4. Experiment

---

## 5. Conclusion