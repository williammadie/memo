# Natural Language Processing

## Table of Content

- [What is NLP](#what-is-nlp)
- [The Process of NLP](#the-process-of-nlp)
    - [Sentence Detection](#sentence-detection)
    - [Tokenization](#tokenization)
    - [Stop Words](#stop-words)
    - [Lemmatization VS Stemming](#lemmatization-vs-stemming)
    - [Word Frequency](#word-frequency)

## What is NLP?

**NLP** stands for **Natural Language Processing**. It is a subfield of Artificial Intelligence and aims at better handling interactions between humans and computers.

**NLP** is the process of *analyzing, understanding and deriving meaning* from human languages for computers.

NLP can be used for *Automatic summarization*, *Question answering systems* or *Question answering systems*

## The Process of NLP

### Sentence Detection

### Tokenization

### Stop Words

**Stop Words** are words that are meaningless. These words depends on the language but are generally articles, prepositions...

They can be removed from the document without affecting further analyzing and processing.

![img_1](/nlp/resources/stopwords.png)

### Lemmatization VS Stemming

Stemming and Lemmatization are both **text normalization techniques** used in NLP. They are used to prepare text, words and documents for further processing.

|                 |                        **Lemmatization**                        |                      **Stemming**                     |
|:---------------:|:---------------------------------------------------------------:|:-----------------------------------------------------:|
|  **Principle**  | combines a **word reduction** and a **morphological analysis**. | is based on **word reduction** until stem is reached. |
|    **Goals**    |               find the most simple form of a word               |              find a common form of words              |
| **Differences** |   always return an existing word / most informative technique   |        much simpler but not as much informative       |
|   **Example**   |                      was, were, been --> be                     |                 informative -> inform                 |

NLP libaries mostly use the **Lemmatization** technique which is considered as far more informative and most suitable to use.

![img_2](/nlp/resources/stemming-vs-lemmatization.png)

### Word Frequency