---
date : '2026-07-12'
draft : false
slug : 'word-embeddings'
categories : 'Natural Language Processing'
summary: 'Converting words into vectors, commonly referred to as word embeddings, is fundamental. These embeddings serve as the foundation for numerous NLP applications, enabling computers to understand and interpret human language.'
description: 'Learn the basics of word embeddings techniques for NLP.'
author : 'Ika Utami'
tags :
    - "Natural Language Processing"
title : 'Word Embeddings Techniques'
ShowReadingTime: true
ShowPostNavLinks: true
---

## Text Representation
In Natural Language Processing (NLP), **computers cannot process text directly because machine learning algorithms operate on numerical data rather than words or sentences**. Consequently, textual information must first be transformed into a numerical representation that preserves as much linguistic information as possible. **This transformation is known as text representation**, and the resulting numerical vectors are commonly referred to as **word embeddings or vector representations**, depending on the technique used.

Text representation forms the foundation of nearly every NLP application, including:
- sentiment analysis
- machine translation
- text classification
- question answering
- information retrieval
- document summarization
- conversational AI 

The quality of these numerical representations significantly influences the performance of downstream machine learning and deep learning models. A well-designed representation captures not only the presence of words but also their **semantic meaning, syntactic relationships, and contextual information**.

Over the years, researchers have developed a variety of techniques for converting text into numerical vectors. Early approaches, such as **One-Hot Encoding, Bag of Words (BoW), N-Grams, and TF-IDF**, represent words or documents using sparse vectors based primarily on word occurrence and frequency. While these methods are simple and computationally efficient, they generally fail to capture **semantic relationships between words**.

To address these limitations, distributed representation methods, commonly known as word embeddings, were introduced. Models such as **Word2Vec, including its Continuous Bag of Words (CBOW) and Skip-Gram architectures**, learn dense vector representations in which semantically similar words are positioned close together in the vector space. These embedding techniques have significantly improved the ability of machines to understand linguistic patterns and have become fundamental components of modern NLP systems.

## 1. One-Hot Encoding
One-Hot Encoding is one of the simplest techniques for representing categorical data, including words, as numerical vectors. In NLP, it converts each unique word in a vocabulary into a binary vector in which exactly one element is 1 (hot) and all remaining elements are 0.

### Advantages
- **Simple and intuitive:** Easy to understand and implement.
- **No training required:** Vectors are generated directly from the vocabulary.
- **Unique representation:** Every word has a distinct vector.
- **Suitable for small vocabularies:** Works well in toy examples and educational settings.

### Disadvantages
- **High dimensionality:** The vector length equals the vocabulary size. Large vocabularies produce very large vectors.
- **Sparse representation:** Most vector elements are zeros, resulting in inefficient memory usage.
- **No semantic information:** Similar words have completely different vectors. For example: cat and dog. Although "cat" and "dog" are semantically related, their vectors are equally distant as any unrelated pair of words.
- **Cannot capture context:** The representation is the same regardless of where the word appears in a sentence.

```python
from sklearn.preprocessing import OneHotEncoder
import numpy as np

# Vocabulary
words = np.array([["cat"], ["dog"], ["bird"], ["fish"]])

encoder = OneHotEncoder(sparse_output=False)
one_hot_vectors = encoder.fit_transform(words)

print(one_hot_vectors)
```

```
[[1. 0. 0. 0.]
 [0. 1. 0. 0.]
 [0. 0. 1. 0.]
 [0. 0. 0. 1.]]
 ```

## 2. Bag of Words (BoW)
Bag of Words (BoW) is one of the most widely used text representation techniques in Natural Language Processing (NLP). It converts a document into a numerical vector by counting the occurrence of each word in a predefined vocabulary. The fundamental assumption of BoW is that **the meaning of a document can be approximated by the frequency of its words**, regardless of their order.

Unlike One-Hot Encoding, which represents individual words, **BoW represents an entire document or sentence as a vector**. Each element of the vector corresponds to a word in the vocabulary, and its value indicates how many times that word appears in the document. One-Hot Encoding creates a unique binary vector for each word, whereas Bag of Words summarizes an entire document by counting the frequency of each vocabulary word. Both methods ignore word order and semantic relationships, but BoW provides richer information by incorporating word frequencies.

The term "Bag of Words" comes from the idea that **all words are placed into a "bag," meaning the original word order, grammar, and sentence structure are ignored. Only the presence or frequency of words is considered**.

### Advantages
- Easy to understand.
- Fast to compute.
- Effective for baseline text classification.

### Disadvantages
- Ignores word order and context.
- Produces sparse vectors.
- Cannot capture semantic similarity.

### How Bag of Words (BoW) Works

The Bag of Words (BoW) model converts text into numerical vectors by counting how many times each word appears in a document.

#### Step 1. Collect Documents

```text
Document 1: I love NLP
Document 2: I love Python
Document 3: Python loves AI
```

#### Step 2. Build the Vocabulary

| Index | Word |
|------:|------|
|0|I|
|1|love|
|2|NLP|
|3|Python|
|4|loves|
|5|AI|

Vocabulary:

```text
[I, love, NLP, Python, loves, AI]
```

#### Step 3. Count Word Frequencies

| Document | I | love | NLP | Python | loves | AI |
|-----------|--:|-----:|----:|-------:|------:|---:|
| Document 1 |1|1|1|0|0|0|
| Document 2 |1|1|0|1|0|0|
| Document 3 |0|0|0|1|1|1|

#### Step 4. Create the Feature Matrix

| Document | Vector |
|-----------|--------|
| Document 1 | [1,1,1,0,0,0] |
| Document 2 | [1,1,0,1,0,0] |
| Document 3 | [0,0,0,1,1,1] |

#### Workflow

```text
Documents
   ↓
Tokenization
   ↓
Build Vocabulary
   ↓
Count Word Frequencies
   ↓
Generate Document Vectors
```

#### Summary

1. Collect documents.
2. Tokenize text.
3. Build the vocabulary.
4. Count word frequencies.
5. Convert each document into a numerical vector.

BoW is simple and effective for traditional machine learning, but it ignores word order and semantic meaning.


## 3. N-Grams
An N-Gram is a contiguous sequence of N consecutive words or characters extracted from a text. In Natural Language Processing (NLP), N-Grams are used to capture local context by preserving the order of neighboring words. Unlike the Bag of Words (BoW) model, which ignores word order entirely, N-Grams retain partial sequential information, making them more informative for many NLP tasks.

The value of N determines the size of the sequence:
- Unigram (N = 1): A single word
- Bigram (N = 2): Two consecutive words
- Trigram (N = 3): Three consecutive words
- 4-gram (N = 4): Four consecutive words
- N-gram (N = N): A sequence of N consecutive words

### Advantages
- Preserves local word order.
- Captures short phrases.
- Improves performance over unigram models.

### Disadvantages
- Feature space grows rapidly.
- Increased memory usage.
- Still limited in long-range context.

### How N-Grams Works
The **N-Gram** model represents text as a sequence of **N consecutive words (or characters)**. Unlike the Bag of Words (BoW) model, which ignores word order, N-Grams preserve the local order of words, allowing the model to capture short phrases and contextual information.

The process of generating N-Grams consists of four main steps.



#### Step 1. Collect the Input Text

Suppose we have the following sentence:

```text
I love Natural Language Processing
```



#### Step 2. Tokenize the Sentence

The sentence is split into individual words (tokens).

```text
[I, love, Natural, Language, Processing]
```

There are **5 tokens** in the sentence.

| Position | Token |
|---------:|-------|
| 1 | I |
| 2 | love |
| 3 | Natural |
| 4 | Language |
| 5 | Processing |



#### Step 3. Choose the Value of N

The value of **N** determines how many consecutive words will be grouped together.

| N | Name | Description |
|---|------|-------------|
| 1 | Unigram | One word |
| 2 | Bigram | Two consecutive words |
| 3 | Trigram | Three consecutive words |
| 4 | Four-gram | Four consecutive words |

For example:

- **N = 2** → Generate **Bigrams**
- **N = 3** → Generate **Trigrams**



**Example for Generating Four-grams (N = 4):**

The sliding window now contains **4 words**.

**Window 1**

```text
[I love Natural Language]
```

**Window 2**

```text
[love Natural Language Processing]
```

Final Four-grams

```text
[I love Natural Language,
 love Natural Language Processing]
```
**Number of N-Grams:**

If a sentence contains **L** words and the N-Gram size is **N**, then the total number of generated N-Grams is

**Number of N-Grams** = L - N + 1

where:

- **L** = Number of words (tokens)
- **N** = Size of the N-Gram

**Example:**

Sentence:

```text
I love Natural Language Processing
```

Number of words:

```text
L = 5
```

| N | Formula | Number of N-Grams |
|---|----------|------------------:|
| 1 | 5 − 1 + 1 | 5 |
| 2 | 5 − 2 + 1 | 4 |
| 3 | 5 − 3 + 1 | 3 |
| 4 | 5 − 4 + 1 | 2 |
| 5 | 5 − 5 + 1 | 1 |

#### Workflow of the N-Gram Model

```text
Input Sentence
        │
        ▼
Tokenize Text
        │
        ▼
Choose N
        │
        ▼
Slide a Window of Size N
        │
        ▼
Generate Consecutive Word Sequences
        │
        ▼
Create N-Gram Features
```

#### Summary of the N-Gram Model

The N-Gram model converts text into sequences of **N consecutive words** by moving a sliding window across the sentence. The process involves:

1. Collecting the input text.
2. Tokenizing the text into individual words.
3. Choosing the value of **N**.
4. Sliding a window of size **N** across the tokens.
5. Generating consecutive word sequences (N-Grams).

Compared with the Bag of Words model, N-Grams preserve the order of neighboring words and capture local contextual information. ***However, they still cannot model long-range dependencies or understand the semantic meaning of words.***


## 4. TF-IDF
TF-IDF (Term Frequency–Inverse Document Frequency) is a statistical text representation technique that **measures how important a word is to a document within a collection (corpus) of documents**. Unlike Bag of Words (BoW), which simply counts word occurrences, TF-IDF assigns a weight to each word based on two factors:

- **Term Frequency (TF):** How often the word appears in a document.
- **Inverse Document Frequency (IDF):** How rare the word is across all documents.

The intuition behind TF-IDF is simple:

- Words that appear frequently in a document are likely to be important for that document.
- Words that appear in many documents (such as the, is, and) are less informative and should receive lower weights.

Thus, TF-IDF gives higher scores to words that are frequent in one document but rare across the entire corpus.

### Why TF-IDF?
Consider the following three documents:
| Document | Text                           |
| -------- | ------------------------------ |
| D1       | I love machine learning        |
| D2       | I love deep learning           |
| D3       | I love artificial intelligence |

Using Bag of Words, the word love appears in every document, so it has the same importance as machine or artificial. However, love does not help distinguish one document from another because it appears everywhere.

TF-IDF solves this problem by:
- Increasing the weight of unique or rare words.
- Decreasing the weight of very common words.

For example:
| Word       | TF-IDF Weight |
| ---------- | ------------: |
| machine    |          High |
| artificial |          High |
| love       |           Low |
| I          |      Very Low |


### Advantages
- Reduces the influence of very common words.
- Highlights informative and distinctive terms.
- Improves text classification and information retrieval.
- Simple to compute and widely supported.
- Works well with traditional machine learning algorithms.

### Disadvantages
- Ignores word order.
- Does not capture semantic meaning.
- Produces sparse vectors for large vocabularies.
- Cannot distinguish different meanings of the same word.
- Cannot capture contextual relationships between words.

### Summary of TF-IDF
TF-IDF improves upon the Bag of Words model by weighting words according to both their frequency within a document and their rarity across the corpus. This enables it to emphasize informative terms while reducing the impact of common words. Although TF-IDF remains a powerful baseline for traditional NLP tasks, it still cannot capture semantic relationships or contextual meaning, which motivated the development of dense word embedding methods such as Word2Vec, GloVe, and contextual models like BERT.

## 5. Word2Vec
Word2Vec is a neural network-based algorithm introduced by researchers at Google in 2013 to learn dense vector representations (word embeddings) of words from large text corpora. Unlike traditional text representation methods such as One-Hot Encoding, Bag of Words (BoW), N-Grams, and TF-IDF, **Word2Vec learns vector representations that capture the semantic and syntactic relationships between words.**

The core idea of Word2Vec is based on the Distributional Hypothesis, which states:

***"Words that appear in similar contexts tend to have similar meanings."***

For example, the words ***king, queen, prince, and princess*** often appear in similar contexts. Therefore, Word2Vec learns vector representations that place these words close together in the embedding space.

Unlike sparse representations where the vector length equals the vocabulary size, Word2Vec generates dense vectors of fixed size (e.g., 100, 200, or 300 dimensions). These vectors contain meaningful numerical values that encode semantic information.

### Why Do We Need Word2Vec?
Earlier text representation methods have several limitations:
| **Method** | **Limitation** |
|------------|----------------|
| **One-Hot Encoding** | Produces **high-dimensional sparse vectors**, where each word is represented independently. It cannot capture semantic or syntactic relationships between words, so similar words (e.g., *car* and *automobile*) have completely different representations. |
| **Bag of Words (BoW)** | Represents documents using **word frequencies** but completely **ignores word order, grammar, and context**. As a result, sentences with different meanings may have identical representations if they contain the same words. |
| **N-Grams** | Preserves **local word order** by considering consecutive word sequences, but it only captures **short-range context**. As the value of *N* increases, the feature space grows exponentially, leading to high memory consumption and data sparsity. |
| **TF-IDF** | Assigns weights based on **word importance** within a document and across a corpus, improving over simple word counts. However, it **cannot capture semantic similarity or contextual meaning**, treating synonyms as unrelated words and producing sparse vector representations. |


### Advantages
- Dense Vector Representation: Word2Vec produces compact vectors (e.g., 100–300 dimensions), reducing memory usage compared with sparse methods.
- Efficient training: Despite using a neural network, Word2Vec is computationally efficient and can be trained on millions of words.
- Captures Semantic Similarity: Words with similar meanings have similar vector representations.
- Captures Syntactic Relationships: The model learns grammatical relationships, such as singular–plural forms and verb tenses.
- Produces high-quality embeddings: Word2Vec embeddings often outperform traditional representations in tasks such as text classification, clustering, and recommendation.

### Disadvantages
- One vector per word. 
Each word has only one vector, regardless of its meaning in different contexts. For example, the word *bank* has the same embedding in: *"I deposited money in the bank."* and *"The fisherman sat on the river bank"*.

- Cannot represent unseen words: Words not seen during training cannot be represented.

- Context-independent: Word2Vec considers only a fixed-size context window and cannot capture long-range dependencies.

- Requires Large Training Data: High-quality embeddings require a large and diverse corpus.

### Summary of Word2Vec
Word2Vec is a neural embedding model that learns dense vector representations of words based on their surrounding context. By leveraging the distributional hypothesis, it captures semantic and syntactic relationships that traditional methods such as One-Hot Encoding, Bag of Words, N-Grams, and TF-IDF cannot represent. Word2Vec has two training architectures - **Continuous Bag of Words (CBOW) and Skip-Gram** - which form the foundation of many modern word embedding techniques. Although Word2Vec produces powerful semantic representations, its embeddings are static and cannot adapt to different contexts, leading to the development of contextual embedding models such as **ELMo, BERT, and GPT**.

## 6. Continuous Bag of Words (CBOW)

### Definition

**Continuous Bag of Words (CBOW)** is one of the two neural network architectures used by the **Word2Vec** algorithm to learn word embeddings. Proposed by Mikolov et al. (2013), CBOW predicts a **target word** based on its surrounding **context words**.

The main idea behind CBOW is based on the **Distributional Hypothesis**, which states that words appearing in similar contexts tend to have similar meanings. By repeatedly predicting a target word from its neighboring words, CBOW learns dense vector representations (embeddings) that capture semantic and syntactic relationships between words.

Unlike traditional text representation methods such as One-Hot Encoding, Bag of Words (BoW), N-Grams, and TF-IDF, CBOW produces **dense, low-dimensional vectors** that preserve semantic similarity between words.

For example, in the sentence

```text
The cat sits on the mat.
```

if the target word is **"sits"** and the context window size is **2**, the surrounding context words are

```text
The   cat   ____   on   the
```

CBOW uses these context words to predict the missing word:

**Input (Context Words)**

```text
The, cat, on, the
```

**Output (Target Word)**

```text
sits
```



### Why CBOW?

Traditional text representation methods have several limitations.

| Method | Limitation |
|--------|------------|
| One-Hot Encoding | Sparse vectors and no semantic information |
| Bag of Words | Ignores word order and context |
| N-Grams | Captures only local context |
| TF-IDF | Measures word importance but not semantic similarity |

CBOW addresses these limitations by learning word representations from the contexts in which words appear.



### How CBOW Works

The CBOW model learns word embeddings through the following steps.

#### Step 1. Prepare the Corpus

Suppose we have the following sentence:

```text
I love studying Natural Language Processing
```



#### Step 2. Tokenize the Sentence

Split the sentence into individual words.

```text
[I, love, studying, Natural, Language, Processing]
```



#### Step 3. Choose the Context Window

The **context window** determines how many neighboring words are used to predict the target word.

Suppose the window size is **2**.

```text
I   love   studying   Natural   Language   Processing
```

Target word:

```text
studying
```

Context words:

```text
I
love
Natural
Language
```

The goal is to predict **studying** from these four surrounding words.



#### Step 4. Convert Words into One-Hot Vectors

Before training, each context word is converted into a **One-Hot Encoding** vector.

Example vocabulary:

| Index | Word |
|------:|------|
|0|I|
|1|love|
|2|studying|
|3|Natural|
|4|Language|
|5|Processing|

The corresponding vectors are

| Word | One-Hot Vector |
|------|----------------|
|I|[1,0,0,0,0,0]|
|love|[0,1,0,0,0,0]|
|Natural|[0,0,0,1,0,0]|
|Language|[0,0,0,0,1,0]|

These vectors are used as inputs to the neural network.



#### Step 5. Project to the Embedding Layer

The one-hot vectors are multiplied by an **embedding matrix**.

Each word is transformed into a dense embedding.

Example:

| Word | Embedding |
|------|-----------|
|I|[0.12, -0.44, 0.61]|
|love|[0.31, 0.20, -0.12]|
|Natural|[-0.25, 0.81, 0.46]|
|Language|[0.54, -0.18, 0.73]|

These vectors are much smaller than one-hot vectors and contain semantic information.



#### Step 6. Average the Context Embeddings

CBOW combines the embeddings of all context words by averaging them.

```text
Embedding(I)
      +
Embedding(love)
      +
Embedding(Natural)
      +
Embedding(Language)
      ------------------------
                4
```

↓

```text
Average Context Vector
```

This vector summarizes the information from the surrounding words.



#### Step 7. Predict the Target Word

The average context vector is passed through the output layer.

A **Softmax** function computes the probability of every word in the vocabulary.

```text
Average Context Vector
          │
          ▼
      Output Layer
          │
          ▼
   Softmax Function
          │
          ▼
 Predicted Target Word
```

The word with the highest probability becomes the prediction.

Example

| Word | Probability |
|------|------------:|
|studying|0.82|
|learning|0.10|
|reading|0.05|
|Natural|0.03|

Predicted word:

```text
studying
```



#### Step 8. Update the Model

The prediction is compared with the correct target word.

If the prediction is incorrect, the model updates its weights using **backpropagation**.

This process repeats millions of times over a large corpus until the embeddings become meaningful.



#### Complete Workflow

```text
Input Sentence
       │
       ▼
Tokenization
       │
       ▼
Choose Context Window
       │
       ▼
Convert Context Words to One-Hot Vectors
       │
       ▼
Embedding Layer
       │
       ▼
Average Context Embeddings
       │
       ▼
Output Layer
       │
       ▼
Softmax Prediction
       │
       ▼
Predicted Target Word
       │
       ▼
Update Embedding Matrix
```



#### Example

Sentence

```text
The cat sits on the mat
```

Window size = **2**

Training sample

| Context Words | Target Word |
|---------------|-------------|
|The, cat, on, the|sits|

Another training sample

Sentence

```text
Machine learning improves education
```

Window size = **1**

| Context Words | Target Word |
|---------------|-------------|
|Machine, improves|learning|
|learning, education|improves|

Each context-target pair becomes one training example.



#### Python Implementation

```python
from gensim.models import Word2Vec

sentences = [
    ["I", "love", "machine", "learning"],
    ["Machine", "learning", "is", "fun"],
    ["I", "enjoy", "learning", "NLP"]
]

model = Word2Vec(
    sentences,
    vector_size=100,
    window=2,
    min_count=1,
    sg=0          # CBOW
)

print(model.wv["learning"])
```



### Advantages

- Learns dense, low-dimensional word embeddings.
- Captures semantic and syntactic relationships between words.
- Faster to train than Skip-Gram.
- Computationally efficient for large datasets.
- Produces high-quality embeddings for frequently occurring words.



### Disadvantages

- Less effective for rare words.
- Ignores the order of context words because it averages their embeddings.
- Produces static embeddings, assigning only one vector to each word regardless of context.
- Limited to a fixed context window and cannot model long-range dependencies.



### Summary of CBOW

The **Continuous Bag of Words (CBOW)** model is one of the two architectures used by Word2Vec to learn word embeddings. It predicts a target word from its surrounding context words by averaging their embeddings and training a shallow neural network. Through this prediction task, CBOW learns dense vector representations in which semantically similar words are located close together in the embedding space. Although CBOW is computationally efficient and performs well for frequent words, it is less effective for rare words and cannot capture different meanings of the same word in different contexts.


## 7. Skip-Gram
**Skip-Gram** is one of the two neural network architectures used by the **Word2Vec** algorithm to learn word embeddings. Unlike the **Continuous Bag of Words (CBOW)** model, which predicts the **target word** from its surrounding context words, Skip-Gram performs the opposite task: it predicts the **surrounding context words** given a **target word**.

The fundamental idea behind Skip-Gram is based on the **Distributional Hypothesis**, which states that words appearing in similar contexts tend to have similar meanings. By learning to predict neighboring words from a target word, Skip-Gram generates dense vector representations (embeddings) that capture semantic and syntactic relationships between words.

For example, consider the sentence:

```text
The cat sits on the mat.
```

If the target word is **"sits"** and the context window size is **2**, the surrounding context words are:

```text
The   cat   sits   on   the
```

**Input (Target Word)**

```text
sits
```

**Output (Context Words)**

```text
The
cat
on
the
```

The Skip-Gram model learns to predict each context word from the target word.

### Why Skip-Gram?

Although CBOW is faster and computationally efficient, it performs less effectively when learning representations for **rare words**.

Skip-Gram addresses this limitation by using each target word to predict multiple surrounding words. Since each occurrence of a word generates several training examples, the model learns richer representations, especially for infrequent words.

Compared with CBOW:

- **CBOW:** Context → Target
- **Skip-Gram:** Target → Context

### How Skip-Gram Works

The Skip-Gram model learns word embeddings through the following steps.

#### Step 1. Prepare the Corpus

Suppose we have the following sentence:

```text
I love studying Natural Language Processing
```

#### Step 2. Tokenize the Sentence

Split the sentence into individual words.

```text
[I, love, studying, Natural, Language, Processing]
```

#### Step 3. Choose the Context Window

Assume the context window size is **2**.

```text
I   love   studying   Natural   Language   Processing
```

Target word

```text
studying
```

Context words

```text
I
love
Natural
Language
```

Unlike CBOW, Skip-Gram uses **"studying"** as the input and predicts each context word individually.

#### Step 4. Convert the Target Word into a One-Hot Vector

Suppose the vocabulary is:

| Index | Word |
|------:|------|
|0|I|
|1|love|
|2|studying|
|3|Natural|
|4|Language|
|5|Processing|

The target word **"studying"** is represented as

| Word | One-Hot Vector |
|------|----------------|
|studying|[0,0,1,0,0,0]|

This one-hot vector is the input to the neural network.

#### Step 5. Project to the Embedding Layer

The one-hot vector is multiplied by the embedding matrix to produce a dense word embedding.

Example:

| Word | Embedding |
|------|-----------|
|studying|[0.42, -0.18, 0.71]|

This dense vector represents the semantic meaning of the target word.

#### Step 6. Predict the Context Words

The embedding is passed through the output layer.

A Softmax function computes the probability of every word in the vocabulary.

The model predicts one surrounding word at a time.

Example

Input

```text
studying
```

Predictions

```text
I
love
Natural
Language
```

Each target-context pair becomes a separate training example.

Training pairs

| Target | Context |
|---------|---------|
|studying|I|
|studying|love|
|studying|Natural|
|studying|Language|

#### Step 7. Update the Model

The predicted context words are compared with the actual context words.

The prediction error is propagated backward using **backpropagation**, updating the embedding matrix.

After training on millions of sentences, words that appear in similar contexts obtain similar embeddings.

#### Complete Workflow

```text
Input Sentence
       │
       ▼
Tokenization
       │
       ▼
Choose Context Window
       │
       ▼
Select Target Word
       │
       ▼
Convert Target Word to One-Hot Vector
       │
       ▼
Embedding Layer
       │
       ▼
Output Layer
       │
       ▼
Softmax Prediction
       │
       ▼
Predict Context Words
       │
       ▼
Update Embedding Matrix
```

#### Example

Sentence

```text
The cat sits on the mat
```

Window size = **2**

Target word

```text
sits
```

Generated training pairs

| Target | Context |
|---------|---------|
|sits|The|
|sits|cat|
|sits|on|
|sits|the|

Another example

Sentence

```text
Machine learning improves education
```

Window size = **1**

Generated training pairs

| Target | Context |
|---------|---------|
|learning|Machine|
|learning|improves|
|improves|learning|
|improves|education|

Each pair is treated as an independent training sample.

#### Python Implementation

```python
from gensim.models import Word2Vec

sentences = [
    ["I", "love", "machine", "learning"],
    ["Machine", "learning", "is", "fun"],
    ["I", "enjoy", "learning", "NLP"]
]

model = Word2Vec(
    sentences,
    vector_size=100,
    window=2,
    min_count=1,
    sg=1          # Skip-Gram
)

print(model.wv["learning"])
```

The parameter `sg=1` tells Word2Vec to use the **Skip-Gram** architecture.

### Advantages

- Learns high-quality word embeddings.
- Better at learning representations for **rare and infrequent words**.
- Captures semantic and syntactic relationships effectively.
- Produces dense, low-dimensional vectors.
- Often performs better than CBOW on smaller datasets.

### Disadvantages

- Slower to train than CBOW because one target word generates multiple prediction tasks.
- Requires more computational resources.
- Produces static embeddings (one vector per word regardless of context).
- Limited to a fixed context window.

### CBOW vs Skip-Gram

| Feature | CBOW | Skip-Gram |
|---------|------|-----------|
| Prediction | Context → Target | Target → Context |
| Input | Context words | Target word |
| Output | One target word | Multiple context words |
| Training speed | Faster | Slower |
| Frequent words | Better | Good |
| Rare words | Moderate | Better |
| Computational cost | Lower | Higher |
| Best suited for | Large datasets | Small datasets and rare words |

### Summary of SkipGram

**Skip-Gram** is one of the two architectures used by the Word2Vec algorithm to learn dense word embeddings. Instead of predicting the target word from its surrounding words, Skip-Gram predicts the surrounding context words from a target word. This approach generates multiple training examples for each target word, enabling the model to learn high-quality embeddings, particularly for rare words. Although Skip-Gram is slower and more computationally expensive than CBOW, it often produces better semantic representations and remains one of the foundational techniques in modern Natural Language Processing.

## 8. Comparison of Text Representation Techniques

The following table summarizes the key characteristics, strengths, and limitations of the most commonly used text representation techniques in Natural Language Processing (NLP).

| Feature | One-Hot Encoding (OHE) | Bag of Words (BoW) | TF-IDF | N-Grams | Word2Vec | CBOW | Skip-Gram |
|---------|-------------------------|--------------------|---------|----------|-----------|------|-----------|
| **Representation Type** | Sparse binary vectors | Sparse count vectors | Sparse weighted vectors | Sparse sequence-based vectors | Dense word embeddings | Dense word embeddings | Dense word embeddings |
| **Represents** | Individual words | Entire documents | Entire documents | Word sequences | Individual words | Individual words | Individual words |
| **Uses Word Frequency** | ❌ | ✅ | ✅ | ✅ | ❌ | ❌ | ❌ |
| **Uses Word Importance** | ❌ | ❌ | ✅ | ❌ | ❌ | ❌ | ❌ |
| **Preserves Word Order** | ❌ | ❌ | ❌ | ✅ (local) | ✅ (through context) | Partially | Partially |
| **Captures Context** | ❌ | ❌ | ❌ | Limited | ✅ | ✅ | ✅ |
| **Captures Semantic Similarity** | ❌ | ❌ | ❌ | ❌ | ✅ | ✅ | ✅ |
| **Captures Syntactic Relationships** | ❌ | ❌ | ❌ | Limited | ✅ | ✅ | ✅ |
| **Vector Type** | Sparse | Sparse | Sparse | Sparse | Dense | Dense | Dense |
| **Vector Dimension** | Vocabulary size | Vocabulary size | Vocabulary size | Vocabulary size (or larger) | Fixed (e.g., 100–300) | Fixed (e.g., 100–300) | Fixed (e.g., 100–300) |
| **Requires Training** | ❌ | ❌ | ❌ | ❌ | ✅ | ✅ | ✅ |
| **Neural Network Based** | ❌ | ❌ | ❌ | ❌ | ✅ | ✅ | ✅ |
| **Handles Rare Words Well** | ❌ | ❌ | ❌ | ❌ | Moderate | Moderate | ✅ |
| **Computational Cost** | Low | Low | Low | Medium | Medium | Low | High |
| **Memory Efficiency** | Poor | Poor | Poor | Poor | Good | Good | Good |
| **Interpretability** | High | High | High | Medium | Low | Low | Low |
| **Typical Applications** | Categorical encoding | Text classification | Information retrieval | Language modeling | Semantic analysis | Large-scale embedding learning | Learning embeddings for rare words |

### Advantages and Disadvantages

| Method | Main Advantages | Main Disadvantages |
|--------|-----------------|--------------------|
| **One-Hot Encoding (OHE)** | Simple, easy to implement, no training required | Produces sparse vectors and cannot capture semantic relationships |
| **Bag of Words (BoW)** | Represents document word frequencies, fast computation | Ignores word order, grammar, and semantic meaning |
| **TF-IDF** | Highlights important words and reduces the influence of common words | Cannot capture semantic similarity or contextual information |
| **N-Grams** | Preserves local word order and captures short phrases | High-dimensional feature space and increased sparsity as *N* grows |
| **Word2Vec** | Learns semantic and syntactic relationships using dense embeddings | Produces static embeddings and requires a large training corpus |
| **CBOW** | Fast training and efficient for learning embeddings of frequent words | Less effective for rare words and ignores the order of context words |
| **Skip-Gram** | Learns high-quality embeddings, especially for rare words | Slower training and higher computational cost than CBOW |

### Choosing the Right Technique

| If your goal is... | Recommended Technique |
|--------------------|-----------------------|
| Encode categorical words | One-Hot Encoding |
| Represent documents using word counts | Bag of Words |
| Identify important words in documents | TF-IDF |
| Preserve short phrases or local word order | N-Grams |
| Learn semantic relationships between words | Word2Vec |
| Train embeddings quickly on a large corpus | CBOW |
| Learn better embeddings for rare words | Skip-Gram |

### Evolution of Text Representation

The development of text representation techniques reflects a progression toward richer linguistic understanding.

```text
One-Hot Encoding
        │
        ▼
Bag of Words (BoW)
        │
        ▼
TF-IDF
        │
        ▼
N-Grams
        │
        ▼
Word2Vec
      ┌─┴─┐
      ▼   ▼
    CBOW Skip-Gram
```

- **One-Hot Encoding** represents each word independently without considering relationships.
- **Bag of Words** improves this by counting word occurrences in documents.
- **TF-IDF** further refines document representation by weighting words according to their importance.
- **N-Grams** preserve local word order by representing sequences of consecutive words.
- **Word2Vec** introduces dense vector representations that capture semantic and syntactic relationships.
- **CBOW** and **Skip-Gram** are the two training architectures used by Word2Vec, each with different strengths depending on the dataset and application.

### Summary

Traditional techniques such as **One-Hot Encoding**, **Bag of Words**, **TF-IDF**, and **N-Grams** represent text using sparse vectors and are effective for many classical machine learning tasks. However, they struggle to capture semantic relationships and contextual meaning.

**Word2Vec** addresses these limitations by learning dense word embeddings from large text corpora. Its two architectures, **CBOW** and **Skip-Gram**, generate meaningful vector representations that place semantically similar words close together in the embedding space. While CBOW is faster and better suited for frequent words, Skip-Gram generally produces higher-quality embeddings for rare words, making both foundational techniques in modern Natural Language Processing.