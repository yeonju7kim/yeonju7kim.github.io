---
layout: post
title: Dec 3th
date: 2023-12-03 00:00:00 +0900
category: InstructBLIP
use_math: true
comments: true
---


# 한 일 정리
- MME coarse benchmark 돌려봄

## 할일 

- POPE 논문 읽기, POPE 사용법 알기
- 논문 작성
  - intro
    - LLM, MLLM
    - Hallucination, research
    - instructblip

## 문제

- text_output을 모름
- issue보자
  - https://github.com/salesforce/LAVIS/issues/125
    - okvqa, vqav2 파인튜닝 방법, format 구현
  - https://github.com/salesforce/LAVIS/issues/198
    - VQA-v2 training details, 왜 none으로 구현됨?
    - > instructBLIP처럼 하네 
  - https://github.com/salesforce/LAVIS/issues/139
    - text split of BLIP-T5, random
  - https://github.com/salesforce/LAVIS/issues/305
    - text_input: "Question: {question} Answer:"
    - text_output returns the answer.
  - https://github.com/salesforce/LAVIS/issues/364
    - image captioning에서 a photo of 를 prefix로 주는 것
  - https://github.com/salesforce/LAVIS/issues/328
    - 배치크기가 크면 학습 안된다
- InstructBLIP은 도대체 어떻게 학습되고 있는거지