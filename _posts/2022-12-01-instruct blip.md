---
layout: post
title: record
date: 2022-12-01 00:00:00 +0900
category: InstructBLIP
use_math: true
comments: true
---


# InstructBLIP

### Abstract

General purpose vision language model 어려움
- rich input distributions and task diversity resulting from the additional visual input
> visual 정보가 너무 rich하고, task도 너무 다양하구나
- 26 datasets을 instruction tuning format으로 만들었구나 
> 이걸 내가 다운받을 수 있으면 좋을텐데

### 1. Introduction

- vl task는 task가 너무 다양
- 보통 2가지 접근
  - multitask learning, 같은 format으로 만듦
  - pretrained llm과 visual 정보, visual 정보는 caption data로 학습
    - broad generalization이 부족
- BLIP-2에서 시작
- instruction tuning할 때 Q-former만 학습 
- 이 논문의 contribution
  - 26 datasets, 11 task categories
  - instruction aware visual feature extraction
  - FlanT5와 Vicuna로 학습

### 2. Vision-Language Instruction Tuning

- 각 테스크별로 10~15 instruction을 생성
  - short, briefly
- 학습
  -  

### 3. Experiment Results and Analysis 

### 4. Related Work

### 5. Conclusion