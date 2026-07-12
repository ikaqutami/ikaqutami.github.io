---
date : '2026-07-12'
draft : false
slug : 'encoder-decoder'
categories : 'Natural Language Processing'
summary: 'The Encoder-Decoder architecture is a neural network framework designed to transform an input sequence into an output sequence. It is one of the most influential architectures in deep learning for sequence-to-sequence (Seq2Seq) tasks, particularly in Natural Language Processing (NLP).'
description: 'Introduction of Encoder and Decoder Architecture.'
author : 'Ika Utami'
tags :
    - "Natural Language Processing"
    - "Encoder-Decoder"
title : 'Encoder-Decoder Architecture (Seq2Seq)'
ShowReadingTime: true
ShowPostNavLinks: true
---

# Encoder–Decoder Architecture

The **Encoder–Decoder architecture** is a neural network framework designed to transform an input sequence into an output sequence. It is one of the most influential architectures in deep learning for **sequence-to-sequence (Seq2Seq)** tasks, particularly in **Natural Language Processing (NLP)**. Unlike traditional machine learning models that map fixed-size inputs to fixed-size outputs, the Encoder–Decoder architecture can process sequences of variable lengths, making it highly suitable for applications such as machine translation, text summarization, dialogue systems, and speech recognition.

The architecture consists of two main components: an **Encoder** and a **Decoder**. 
- The encoder is responsible for understanding the input sequence and compressing its information into a meaningful representation.
- The decoder generates the target sequence based on that representation.

---

# Motivation

Many NLP tasks require converting one sequence into another. For example:

- Translating a sentence from English to French.
- Summarizing a long document into a short paragraph.
- Generating a response in a chatbot.
- Converting speech into text.

In these tasks, the lengths of the input and output sequences are often different. Traditional neural networks cannot effectively handle this problem because they require fixed-size inputs and outputs. The Encoder–Decoder architecture overcomes this limitation by learning a mapping between variable-length sequences.

---

# Components of Encoder–Decoder Architecture

## Encoder

The **Encoder** is the first part of the architecture. Its primary purpose is to read the input sequence and convert it into a numerical representation that captures the semantic meaning of the entire sequence.

The encoder processes one token at a time. Each input token is transformed into an embedding vector and passed through recurrent units such as **RNN**, **LSTM**, or **GRU**. As the encoder processes each token, it continuously updates its hidden state. The final hidden state represents a compressed summary of the input sequence and is commonly referred to as the **context vector**.

For example, consider the input sentence:

> *I love deep learning.*

The encoder reads the words sequentially:

1. I
2. love
3. deep
4. learning

After processing all words, the encoder produces a context vector containing information about the meaning of the entire sentence.

### Functions of the Encoder

- Reads the input sequence.
- Learns contextual information.
- Produces hidden states.
- Generates the context vector representing the input.

### Advantages

- Captures semantic information from the input sequence.
- Supports variable-length inputs.
- Works well with sequential data.

### Limitations

- Compressing long sequences into a single context vector may result in information loss.
- Performance decreases as sequence length increases.
- Motivated the development of attention mechanisms.

---

## Context Vector

The **Context Vector** is the intermediate representation that connects the encoder and decoder. It is a dense vector containing information extracted from the input sequence.

In the original Seq2Seq architecture, only the encoder's final hidden state is passed to the decoder as the context vector. This vector serves as the decoder's initial state and guides the generation of the output sequence.

Although effective for short sequences, a single context vector often struggles to represent long or complex sentences because all information must be compressed into one fixed-length vector.

### Characteristics

- Fixed-length representation.
- Encodes semantic information.
- Bridges the encoder and decoder.
- May lose information for long sequences.

---

## Decoder

The **Decoder** is responsible for generating the target sequence one token at a time based on the context vector received from the encoder.

At the beginning of decoding, the context vector initializes the decoder's hidden state. The decoder then predicts the first output token. Each predicted token is fed back into the decoder to generate the next token until a special **End-of-Sequence (EOS)** token is produced.

For example, if the input sentence is:

> *I love deep learning.*

the decoder may generate:

> *J'aime l'apprentissage profond.*

Each generated word depends on both the context vector and the previously generated words.

### Functions of the Decoder

- Generates the output sequence.
- Predicts one token at a time.
- Uses previous outputs to generate subsequent tokens.
- Stops when the EOS token is generated.

### Advantages

- Produces variable-length outputs.
- Learns sequential dependencies.
- Suitable for text generation tasks.

### Limitations

- Early prediction errors may propagate to later predictions.
- Depends heavily on the quality of the context vector.

---

# Sequence-to-Sequence (Seq2Seq) Learning

The Encoder–Decoder architecture is commonly known as the **Sequence-to-Sequence (Seq2Seq)** model because it maps one sequence into another.

The learning process consists of two stages:

1. **Encoding Stage**
   - The encoder processes the entire input sequence.
   - Hidden states are updated at every time step.
   - The final hidden state becomes the context vector.

2. **Decoding Stage**
   - The decoder initializes its hidden state using the context vector.
   - Output tokens are generated sequentially.
   - Generation continues until the EOS token is produced.

---

# Training the Encoder–Decoder Model

During training, the decoder often uses a technique called **Teacher Forcing**. Instead of using its own predicted token as the next input, the decoder receives the actual target token from the training data.

Teacher forcing accelerates convergence and stabilizes training because the decoder always receives the correct previous token. However, during inference, the correct target tokens are unavailable, so the decoder must rely on its own predictions. This mismatch between training and inference is known as **Exposure Bias**.

---

# Attention Mechanism

One limitation of the original Encoder–Decoder architecture is that the decoder relies entirely on a single context vector. As input sequences become longer, this fixed-size representation may fail to capture all important information.

The **Attention Mechanism** addresses this problem by allowing the decoder to access all encoder hidden states rather than only the final one. At each decoding step, the decoder computes attention weights that determine which parts of the input sequence are most relevant for generating the current output token.

For example, when translating:

> *The cat sits on the mat.*

the decoder can focus on different words depending on which target word is being generated.

Benefits of attention include:

- Better handling of long sequences.
- Improved translation quality.
- Richer contextual representation.
- Higher prediction accuracy.

The attention mechanism became the foundation for modern Transformer architectures.

---

# Applications of Encoder–Decoder Architecture

The Encoder–Decoder framework has been successfully applied to numerous sequence generation tasks, including:

- Machine Translation
- Text Summarization
- Question Answering
- Dialogue Systems and Chatbots
- Speech Recognition
- Image Captioning
- Grammar Correction
- Code Generation
- Text Simplification

---

# Advantages

- Handles variable-length input and output sequences.
- Learns contextual representations automatically.
- Effective for sequence generation tasks.
- Flexible architecture that can be implemented using RNN, LSTM, GRU, or Transformer models.
- Forms the foundation of many modern NLP systems.

---

# Limitations

- Original Seq2Seq models struggle with long input sequences.
- Information bottleneck caused by the fixed-length context vector.
- Sequential computation limits parallelization when implemented with RNNs.
- Exposure bias may reduce inference performance.
- Training can be computationally expensive for long sequences.

---

# Evolution of Encoder–Decoder Architecture

The Encoder–Decoder architecture has evolved significantly over time:

| Generation | Encoder | Decoder | Main Improvement |
|------------|---------|---------|------------------|
| Seq2Seq (2014) | RNN | RNN | First sequence-to-sequence model |
| Seq2Seq + LSTM | LSTM | LSTM | Better long-term dependency learning |
| Seq2Seq + GRU | GRU | GRU | Faster training with fewer parameters |
| Seq2Seq + Attention | LSTM/GRU | LSTM/GRU | Access to all encoder hidden states |
| Transformer | Self-Attention | Self-Attention | Parallel computation and superior performance |

---

# Summary

The Encoder–Decoder architecture is a fundamental framework for sequence-to-sequence learning. It consists of an encoder that converts an input sequence into a contextual representation and a decoder that generates the target sequence based on that representation. Originally implemented using recurrent neural networks such as RNNs, LSTMs, and GRUs, the architecture demonstrated remarkable success in tasks such as machine translation and text generation.

However, the fixed-length context vector introduced an information bottleneck for long sequences. This limitation was overcome by the introduction of the **Attention Mechanism**, which enabled the decoder to selectively focus on different parts of the input during generation. Attention later became the core principle behind the **Transformer architecture**, which has become the dominant model for modern NLP applications due to its ability to process sequences in parallel and capture long-range dependencies efficiently.