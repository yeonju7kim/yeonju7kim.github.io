---
layout: post
title: (AI502) 4. recurrent_neural_networks
date: 2022-03-31 00:10:00 +0900
category: class-summary
use_math: true
comments: true
---

본 포스팅은 AI502수업에서 제가 새로 알게 된 부분만 정리한 것입니다.

---

## RNN

- timestamp가 있으면 RNN 사용한다.
- 주로 cross entropy loss를 사용한다.
- Vanishing gradient 
  - long term dependency를 학습하지 못함
  - Initialization을 identity matrix로 하고 + ReLU activation
  - regularizer
    - ![alt image](/public/img/220331/regularizer.png)
  - skip-connections
    - Leaky units
- Gradient Clipping
  - exploding gradient를 막음
  - normalize the gradient
  - $\rVert g \rVert \gt v, g \leftarrow \frac{g_v}{\rVert g \rVert}$
- Long term, short term dependency 둘다 학습
  - clockwork RNN
- Recursive Neural Network
  - depth를 줄인다.

## LSTM

- cell state : highway가 있어서 필요할 때만 modify한다.
- forget gate
- input gate
- output gate

## GRU

- update gate : forget + input
- reset gate

## Bidirectional RNNs

## Deep Recurrent Networks

- hidden layer
- input-hidden, hidden-hidden, hidden-output
- + skip connection

## Deep (Bidirectional) Recurrent Networks

## Attention

- hidden states의 weight를 학습
- hidden states간의 관계를 학습
- robust to the length
- hard attention vs soft attention
  - hard : 0, 1
  - soft : 0 ~ 1
- Scaled Dot-Product attention
  - ![alt image](/public/img/220331/attention.png) 