---
date : '2026-07-12T20:03:13+07:00'
draft : false
slug : 'transformer-intro'
categories : 'Natural Language Processing'
summary: 'Transformers are a foundational deep learning architecture in Natural Language Processing (NLP) that process entire sentences simultaneously. Using self-attention mechanisms, they analyze how every word relates to every other word in a text, enabling machines to understand deep context and generate human-like language.'
description: 'Transformer Introduction'
author : 'Ika Utami'
tags :
    - "Natural Language Processing"
    - "Transformer"
title : 'Transformer'
ShowReadingTime: true
ShowPostNavLinks: true
---

# Transformer Architecture

The **Transformer architecture** is a deep learning model introduced by Vaswani et al. in the landmark 2017 paper *"Attention Is All You Need."* It revolutionized Natural Language Processing (NLP) by replacing recurrent neural networks (RNNs) and convolutional neural networks (CNNs) with a mechanism based entirely on **attention**. Unlike previous sequence models that process input tokens sequentially, Transformers process all tokens simultaneously, enabling efficient parallel computation and significantly reducing training time.

Since its introduction, the Transformer has become the foundation of nearly all modern NLP models, including **BERT**, **GPT**, **T5**, **RoBERTa**, **BART**, and **LLaMA**. Beyond NLP, Transformer-based architectures have also been successfully applied to computer vision, speech recognition, recommendation systems, and multimodal learning.

---

# Motivation

Before the Transformer architecture, sequence modeling was primarily performed using recurrent neural networks such as **RNNs**, **LSTMs**, and **GRUs**. Although these models were effective for many tasks, they suffered from several limitations.

First, recurrent models process tokens sequentially, meaning that each word must wait for the previous word to be processed before computation can continue. This sequential dependency prevents efficient parallelization and significantly increases training time.

Second, although LSTMs and GRUs improve upon traditional RNNs, they still struggle to capture very long-range dependencies within long sequences. Information from earlier tokens may gradually weaken as the sequence grows longer.

The Transformer was designed to overcome these challenges by relying entirely on the **Self-Attention Mechanism**, allowing every token in a sequence to directly interact with every other token regardless of their distance.

---

# Overview of the Transformer Architecture

The original Transformer consists of two major components:

- **Encoder**
- **Decoder**

The encoder converts the input sequence into contextual representations, while the decoder generates the output sequence based on those representations.

```
Input Sequence
       │
       ▼
+-----------------+
|     Encoder     |
+-----------------+
       │
 Contextual Representation
       │
       ▼
+-----------------+
|     Decoder     |
+-----------------+
       │
       ▼
Output Sequence
```

The encoder and decoder are each composed of multiple identical layers stacked on top of one another.

In the original Transformer model:

- Encoder: 6 layers
- Decoder: 6 layers

Modern Transformer variants often use dozens or even hundreds of layers depending on the application.

---

# Components of the Transformer

## Input Embedding

Neural networks cannot process text directly. Therefore, each input token is first converted into a dense numerical vector known as an **embedding**.

For example, the sentence

> *I love NLP.*

may first be tokenized as:

```
["I", "love", "NLP", "."]
```

Each token is then mapped into a continuous embedding vector.

These embeddings capture semantic relationships between words, allowing similar words to have similar vector representations.

---

## Positional Encoding

Unlike RNNs, Transformers process all tokens simultaneously. Consequently, they have no inherent understanding of word order.

To provide information about token positions, Transformers add **Positional Encoding** to each embedding.

Positional encodings enable the model to distinguish between sentences such as:

- Dog bites man.
- Man bites dog.

Although both sentences contain the same words, their meanings differ because of word order.

Positional encoding can be either:

- Fixed sinusoidal encoding (original Transformer)
- Learned positional embeddings

Adding positional information allows the model to preserve sequence order while maintaining parallel computation.

---

## Multi-Head Self-Attention

The **Multi-Head Self-Attention** mechanism is the core component of the Transformer.

Rather than processing words sequentially, self-attention enables every token to examine every other token in the sequence simultaneously.

For example, in the sentence

> *The animal didn't cross the street because it was tired.*

the model learns that the word **"it"** refers to **"animal"**, even though several words separate them.

Instead of using a single attention mechanism, the Transformer employs multiple attention heads running in parallel.

Each attention head learns different types of relationships, such as:

- Semantic relationships
- Grammatical dependencies
- Long-distance context
- Syntactic structure

The outputs from all attention heads are combined to produce a richer contextual representation.

### Advantages

- Captures long-range dependencies.
- Enables parallel computation.
- Learns multiple contextual relationships simultaneously.
- Improves language understanding.

---

## Feed-Forward Neural Network

After self-attention, each token representation passes through a **Feed-Forward Neural Network (FFN)**.

The FFN consists of two fully connected layers separated by a nonlinear activation function, typically ReLU or GELU.

Unlike self-attention, which allows interactions between different tokens, the feed-forward network processes each token independently while increasing the model's representational capacity.

---

## Residual Connections

Deep neural networks often suffer from optimization difficulties as they become deeper.

To address this issue, Transformers use **Residual Connections**, also known as skip connections.

Instead of learning an entirely new representation, each layer learns a refinement of the previous representation.

Residual connections improve gradient flow and stabilize training, making very deep Transformer models possible.

---

## Layer Normalization

Each sublayer in the Transformer is followed by **Layer Normalization**.

Layer normalization standardizes the activations across hidden dimensions, reducing internal covariate shift and improving training stability.

Benefits include:

- Faster convergence.
- More stable optimization.
- Better generalization.

---

# Encoder Architecture

Each encoder layer consists of:

1. Multi-Head Self-Attention
2. Add & Layer Normalization
3. Feed-Forward Network
4. Add & Layer Normalization

```
Input
  │
  ▼
Multi-Head Self-Attention
  │
  ▼
Add & LayerNorm
  │
  ▼
Feed Forward Network
  │
  ▼
Add & LayerNorm
  │
Output
```

The encoder transforms the input sequence into contextual representations that capture relationships between all input tokens.

---

# Decoder Architecture

Each decoder layer contains three main sublayers:

1. Masked Multi-Head Self-Attention
2. Encoder–Decoder Attention
3. Feed-Forward Network

The masked attention mechanism prevents the decoder from seeing future tokens during training, ensuring that predictions remain autoregressive.

Encoder–Decoder Attention enables the decoder to attend to encoder outputs while generating each target token.

---

# Self-Attention Computation

Self-attention is computed using three vectors:

- **Query (Q)**
- **Key (K)**
- **Value (V)**

Each token generates its own Query, Key, and Value vectors.

The similarity between queries and keys determines how much attention each token should receive.

The attention score is computed as:

\[
\text{Attention}(Q,K,V)=
\text{Softmax}
\left(
\frac{QK^T}{\sqrt{d_k}}
\right)V
\]

where:

- **Q** = Query matrix
- **K** = Key matrix
- **V** = Value matrix
- **dₖ** = dimensionality of Key vectors

The scaling factor prevents extremely large attention scores during training.

---

# Training the Transformer

During training, the Transformer typically uses **Teacher Forcing**, where the decoder receives the correct previous token rather than its own prediction.

The objective is to minimize the prediction error using **Cross-Entropy Loss**, while optimization is commonly performed using the **Adam** optimizer with learning rate scheduling.

Because all tokens can be processed simultaneously, Transformer training is significantly faster than recurrent models.

---

# Applications of Transformer Architecture

Transformers have become the standard architecture for numerous artificial intelligence applications, including:

- Machine Translation
- Text Summarization
- Text Classification
- Question Answering
- Chatbots
- Language Modeling
- Named Entity Recognition
- Sentiment Analysis
- Speech Recognition
- Image Captioning
- Code Generation
- Vision Transformers (ViT)
- Multimodal Learning

---

# Advantages

- Processes sequences in parallel.
- Captures long-range dependencies effectively.
- Eliminates the vanishing gradient problems associated with recurrent networks.
- Highly scalable to very large datasets.
- Produces state-of-the-art performance on many NLP benchmarks.
- Forms the foundation of modern large language models (LLMs).

---

# Limitations

- Self-attention has quadratic computational complexity with respect to sequence length.
- Memory consumption increases rapidly for long documents.
- Requires substantial computational resources for training.
- Large Transformer models demand significant storage and inference resources.

---

# Evolution of Transformer Models

| Model | Main Contribution |
|--------|-------------------|
| Transformer (2017) | Introduced self-attention as the primary sequence modeling mechanism |
| BERT | Bidirectional encoder for language understanding |
| GPT | Decoder-only architecture for autoregressive text generation |
| RoBERTa | Improved BERT training strategy |
| T5 | Unified text-to-text framework |
| BART | Encoder–decoder Transformer for generation and understanding |
| Vision Transformer (ViT) | Applied Transformers to computer vision |
| LLaMA | Efficient large language models for research and deployment |

---

# Transformer vs. RNN-Based Models

| Feature | RNN/LSTM/GRU | Transformer |
|----------|--------------|-------------|
| Processing | Sequential | Parallel |
| Long-Term Dependency | Moderate | Excellent |
| Training Speed | Slow | Fast |
| Parallelization | Limited | Excellent |
| Memory for Long Sequences | Limited | Better contextual modeling |
| Core Mechanism | Recurrence | Self-Attention |

---

# Summary

The **Transformer architecture** represents a major breakthrough in deep learning by replacing recurrent computations with self-attention mechanisms. Instead of processing tokens one at a time, Transformers allow every token in a sequence to attend to every other token simultaneously, enabling efficient parallel computation and improved modeling of long-range dependencies.

A Transformer consists of an encoder that learns contextual representations of the input sequence and a decoder that generates the output sequence. Key components such as **Input Embedding**, **Positional Encoding**, **Multi-Head Self-Attention**, **Feed-Forward Networks**, **Residual Connections**, and **Layer Normalization** work together to produce highly expressive representations of language.

The Transformer has become the foundation of modern NLP and artificial intelligence. Most state-of-the-art language models—including **BERT**, **GPT**, **T5**, and **LLaMA**—are built upon Transformer architectures, making it one of the most influential innovations in machine learning.