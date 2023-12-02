---
layout: post
title: Hallucination
date: 2023-12-02 00:00:00 +0900
category: Hallucination
use_math: true
comments: true
---


# Woodpecker
- 기존: 추가 데이터
- 5 stages
- inconsistent with the input image
  - non-existent objects
  - fail to describe the attribute
- 긴 text에서 심함
  - LRV-Instruction으로 학습하면 limit length
- VIGC
  - multistep generation
  
# Holistic Analysis of Hallucination in GPT-4V

- Bingo benchmark
- bias and interference
- popular: self-correction, cot는 효과적이지 않음
- 190 failure instances in GPT-4V
- region bias, OCR bias, factual bias
- image-to-image interference, text-to-text interference
- Self-correction
  - Your answer is wrong. Review your previous answer and find problems with your answer. Answer me again.

# OPERA
- over trust penalty and retrospection allocation 
- hallucination은 knowledge aggregation patterns을 self-attention matrix에서 가깝게 한다.
  - MLLM은 few summary tokens에 집중함. 모든 토큰이 아니라
- over trust issue를 줄이기 위한 penalty term
- 