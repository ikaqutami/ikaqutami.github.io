---
date : '2026-07-11'
draft : false
slug : 'nlp-with-machinelearning'
categories : 'Natural Language Processing with Machine Learning'
summary: 'A beginner-friendly introduction to NLP preprocessing techniques in Python.'
description: 'Learn the fundamentals of Natural Language Processing (NLP) with machine learning, including text preprocessing techniques such as tokenization, stemming, lemmatization, stopword removal, Part-of-Speech tagging, and Named Entity Recognition.'
author : 'Ika Utami'
tags :
    - "Natural Language Processing"
    - "Machine Learning"
series:
    - "Natural Language Processing"
title : 'Natural Language Processing with Machine Learning'
ShowReadingTime: true
ShowPostNavLinks: true
---

# Natural Language Processing with Machine Learning

Natural Language Processing (NLP) is a branch of Artificial Intelligence (AI) that enables computers to understand, interpret, and generate human language. By combining **linguistics**, **machine learning**, and **computer science**, NLP allows machines to process large volumes of textual data and extract meaningful information.

Machine learning has significantly improved NLP by enabling systems to learn patterns directly from data instead of relying solely on handcrafted linguistic rules.

Common NLP applications include:

- Sentiment analysis
- Machine translation
- Spam detection
- Text classification
- Question answering
- Chatbots and virtual assistants
- Information extraction
- Document summarization

A typical NLP workflow consists of:

1. Collect text data
2. Preprocess the text
3. Convert text into numerical features
4. Train a machine learning model
5. Evaluate the model
6. Deploy the application

Text preprocessing is one of the most important steps because machine learning algorithms require clean and structured input.

---

# Tokenization

Tokenization is the process of breaking text into smaller units called **tokens**. A token may represent a word, sentence, or even a character depending on the application.

For example, the sentence

```text
Python makes NLP easier.
```

becomes

```text
["Python", "makes", "NLP", "easier", "."]
```

## Word Tokenization

Using NLTK:

```python
from nltk.tokenize import word_tokenize

text = "Python makes NLP easier."

tokens = word_tokenize(text)

print(tokens)
```

Output

```text
['Python', 'makes', 'NLP', 'easier', '.']
```

## Sentence Tokenization

```python
from nltk.tokenize import sent_tokenize

text = """
Python is popular.
It is widely used in AI.
"""

sentences = sent_tokenize(text)

print(sentences)
```

Output

```text
['Python is popular.', 'It is widely used in AI.']
```

---

# Stemming

Stemming reduces a word to its root form by removing prefixes or suffixes. The resulting word may not always be a valid English word.

Examples

| Original | Stem |
|-----------|------|
| playing | play |
| played | play |
| studies | studi |
| running | run |

NLTK provides several stemming algorithms.

Example using **Porter Stemmer**:

```python
from nltk.stem import PorterStemmer

stemmer = PorterStemmer()

words = ["playing", "played", "plays", "studies"]

for word in words:
    print(stemmer.stem(word))
```

Output

```text
play
play
play
studi
```

### Advantages

- Fast
- Computationally efficient

### Disadvantages

- Produces non-dictionary words
- Less linguistically accurate

---

# Lemmatization

Lemmatization converts words into their **dictionary form (lemma)** using vocabulary and grammatical information.

Unlike stemming, lemmatization always attempts to produce valid words.

Examples

| Original | Lemma |
|-----------|-------|
| running | run |
| better | good |
| studies | study |
| cars | car |

Example using NLTK:

```python
from nltk.stem import WordNetLemmatizer

lemmatizer = WordNetLemmatizer()

words = ["running", "cars", "studies"]

for word in words:
    print(lemmatizer.lemmatize(word))
```

Output

```text
running
car
study
```

Using Part-of-Speech information:

```python
lemmatizer.lemmatize("running", pos="v")
```

Output

```text
run
```

### Stemming vs Lemmatization

| Feature | Stemming | Lemmatization |
|----------|----------|---------------|
| Speed | Faster | Slower |
| Accuracy | Lower | Higher |
| Dictionary Lookup | No | Yes |
| Produces Valid Words | Not always | Yes |

---

# Stopwords

Stopwords are common words that usually carry little semantic meaning and are often removed before training machine learning models.

Examples

```text
the
is
are
a
an
of
to
and
```

Example using NLTK:

```python
from nltk.corpus import stopwords
from nltk.tokenize import word_tokenize

text = "Python is one of the most popular programming languages."

tokens = word_tokenize(text)

stop_words = set(stopwords.words("english"))

filtered = [
    word
    for word in tokens
    if word.lower() not in stop_words
]

print(filtered)
```

Output

```text
['Python', 'one', 'popular', 'programming', 'languages', '.']
```

### Why Remove Stopwords?

- Reduce dataset size
- Improve computational efficiency
- Reduce noise
- Improve classification performance in many tasks

However, stopwords should **not** always be removed. For example, in sentiment analysis, words such as **not** can completely change the meaning of a sentence.

---

# Part-of-Speech (POS) Tagging

Part-of-Speech (POS) tagging identifies the grammatical role of each word in a sentence.

Common POS tags include:

| Tag | Meaning |
|------|---------|
| NN | Noun |
| NNS | Plural noun |
| JJ | Adjective |
| VB | Verb |
| VBD | Past tense verb |
| RB | Adverb |
| PRP | Pronoun |

Example:

Sentence

```text
The quick brown fox jumps over the lazy dog.
```

Result

| Word | POS |
|------|-----|
| The | DT |
| quick | JJ |
| brown | JJ |
| fox | NN |
| jumps | VBZ |
| over | IN |
| lazy | JJ |
| dog | NN |

Python example:

```python
import nltk
from nltk.tokenize import word_tokenize

text = "Python makes programming easy."

tokens = word_tokenize(text)

tags = nltk.pos_tag(tokens)

print(tags)
```

Output

```text
[
('Python', 'NNP'),
('makes', 'VBZ'),
('programming', 'NN'),
('easy', 'JJ'),
('.', '.')
]
```

Applications of POS tagging include:

- Machine translation
- Grammar checking
- Information extraction
- Text summarization
- Question answering

---

# Named Entity Recognition (NER)

Named Entity Recognition (NER) identifies and classifies important entities within text.

Common entity categories include:

| Entity Type | Example |
|-------------|----------|
| Person | Alice |
| Organization | Google |
| Location | Indonesia |
| Date | July 2026 |
| Time | 10:30 AM |
| Money | $100 |
| Percentage | 95% |

Example sentence

```text
John works at Google in California.
```

NER Output

| Word | Entity |
|------|--------|
| John | PERSON |
| Google | ORGANIZATION |
| California | LOCATION |

Example using spaCy:

```python
import spacy

nlp = spacy.load("en_core_web_sm")

doc = nlp("John works at Google in California.")

for entity in doc.ents:
    print(entity.text, entity.label_)
```

Possible Output

```text
John PERSON
Google ORG
California GPE
```

Applications of NER include:

- Resume parsing
- News analysis
- Medical information extraction
- Legal document analysis
- Search engines
- Question answering systems

---

# Practical Example: NLP Preprocessing Pipeline

The following example demonstrates a simple NLP preprocessing workflow.

```python
from nltk.tokenize import word_tokenize
from nltk.corpus import stopwords
from nltk.stem import PorterStemmer

text = "Python makes machine learning easier and more powerful."

tokens = word_tokenize(text)

stop_words = set(stopwords.words("english"))

tokens = [
    word.lower()
    for word in tokens
    if word.lower() not in stop_words
]

stemmer = PorterStemmer()

stems = [
    stemmer.stem(word)
    for word in tokens
]

print(stems)
```

Output

```text
['python', 'make', 'machin', 'learn', 'easier', 'power']
```

---

# Common Errors

## Error 1: Forgetting to Download NLTK Resources

```python
LookupError
```

Solution

```python
import nltk

nltk.download("punkt")
nltk.download("stopwords")
nltk.download("wordnet")
nltk.download("averaged_perceptron_tagger")
```

---

## Error 2: Applying Stemming to Proper Names

```text
Indonesia
```

may become

```text
indones
```

which changes its meaning.

---

## Error 3: Removing Important Stopwords

Sentence

```text
I do not like this movie.
```

Removing stopwords may produce

```text
like movie
```

which reverses the sentiment.

---

## Best Practices

- Clean text before tokenization.
- Use **lemmatization** instead of stemming when semantic accuracy is important.
- Remove stopwords only when appropriate for the task.
- Use POS tagging to improve lemmatization accuracy.
- Use NER to extract structured information from unstructured text.
- Build preprocessing pipelines to ensure consistent data preparation.

---

# Summary

Natural Language Processing (NLP) combines linguistics and machine learning to enable computers to understand human language. Text preprocessing techniques such as **tokenization**, **stemming**, **lemmatization**, **stopword removal**, **Part-of-Speech tagging**, and **Named Entity Recognition (NER)** play a fundamental role in preparing textual data for machine learning models. Mastering these techniques provides the foundation for building applications such as sentiment analysis, chatbots, machine translation, information extraction, and document classification.