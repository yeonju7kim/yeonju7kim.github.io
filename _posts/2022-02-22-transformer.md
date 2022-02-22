---
layout: post
title: Transformer
date: 2022-02-22 00:00:00 +0900
category: dl_paper
---
본 포스팅은 아래 논문을 참고했습니다.
<https://arxiv.org/pdf/1706.03762.pdf>

# Transformer

## Introduction

RNN은 sequence의 길이가 길 때 취약하다는 문제가 있었다. 이 문제를 해결하기 위해 factorization trick, conditional computation 등의 최근의 시도가 있었다. 하지만 sequential computation이 가지는 한계는 여전했다.<br>

본 논문에서는 이런 문제를 해결하기 위해 Transformer라는 구조를 제안했다. 이는 Recurrene는 피하고, input과 output의 global dependency를 이끌기 위해 attention mechanism에 전적으로 의존하는 구조이다.

---

## Background

- 연속적인 계산을 줄이기 위해 Extended Neural GPU, ByteNet, ConvS2S 등이 나왔다. 이것은 input과 output에 hidden representation을 parallel하게 계산했다. 이것은 distant position의 의존도를 학습하기 어려웠다.
- Self-attention(intra-attention) : single sequence의 다른 position과 관련된 attention machanism
- Transformer는 RNN과 CNN을 사용하지 않고, self-attention만을 이용하는 첫 transduction model

---

## Model Architecture

![alt text](/public/img/220222/transformer_architecture.PNG)

#### encoder-decoder 구조
>
> - stacked self-attention
> - point-wise, fc layer 사용

#### Encoder
>
> - 6 layers
> - 2 sub layer
>   - multi-head self-attention
>   - simple, position-wise fully connected feed-forward network
>   - 각 sub layer 뒤에 residual connection, layer normalization
>   - 모든 sub layer의 output과 embedding layer의 output은 d_model(512)으로 맞춤

#### Decoder
>
> - 6 layers
> - 3 sub layer
>   - multi-head attetion 2개
>   - feed-forward network 1개
>   - 각 sub layer 뒤에 residual connection, layer normalization
>   - 모든 sub layer의 output과 embedding layer의 output은 d_model(512)으로 맞춤
>   - masking : This masking, combined with fact that the output embeddings are offset by one position, ensures that the predictions for position i can depend only on the known outputs at positions less than i (이해 못함)

#### Scaled Dot-Product Attention
>
> 흔히 사용되는 attension function은 2 종류 (additive attention, dot-product attention)<br>
> 논문에서는 additive attention에서 scaling factor를 추가해서 사용<br>
> $$scaling factor=\frac{1}{\sqrt{d_k}}$$
>
> dot-product attetion : faster, more space-efficient<br>
> additive attention : d_k가 크면 성능 좋음
>
> $$ Attension(Q, K, V) = softmax(\frac{QK^T}{\sqrt{d_k}})V $$
>

#### Multi-Head Attention

> ![alt text](/public/img/220222/multihead_attention.PNG)
> 결국 MultiHead Attention Energy는 d_model x d_model 이 나오고, i번째 attention은 d_model x h가 나온다. 그리고

#### Multi-Head Attention을 쓰는 3가지 방법
>
> 1. encoder-decoder attention : decoder에서 query를 얻고, encoder에서 key와 value를 얻는다. 하나의 query를 각 key와 value에 적용한다.
> 2. encoder contains self-attention layers : 
> 3. self-attention layers in the decoder : 

---

##

---

##

---

##

##
