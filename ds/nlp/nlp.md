# Natural Language Processing

## Table of Content

- [What is NLP](#what-is-nlp)
- [The Process of NLP](#the-process-of-nlp)
    - [Sentence Detection](#sentence-detection)
    - [Tokenization](#tokenization)
    - [Stop Words](#stop-words)
    - [Lemmatization VS Stemming](#lemmatization-vs-stemming)
    - [Word Frequency](#word-frequency)
- [Training a ML algorithm](#training-a-ml-algorithm)
    - [Bags of words](#bags-of-words)

## What is NLP?

**NLP** stands for **Natural Language Processing**. It is a subfield of Artificial Intelligence and aims at better handling interactions between humans and computers.

**NLP** is the process of *analyzing, understanding and deriving meaning* from human languages for computers.

NLP can be used for *Automatic summarization*, *Question answering systems* or *Question answering systems*

## The Process of NLP

### Sentence Detection

### Tokenization

Tokenization is the process of splitting a string into meaningful units (*words, punctuation characters, numbers*).

```python
input_sentence = "What would you do with 100000$?"

tokenized_array = ["what", "would", "you", "do", "with", "100000", "$", "?"]
```

### Stop Words

**Stop Words** are words that are meaningless. These words depends on the language but are generally articles, prepositions...

They can be removed from the document without affecting further analyzing and processing.

![img_1](/ds/nlp/resources/stopwords.png)

### Stemming

Stemming is the process of generating the root form of the words. It is a heuristic algorithm that chops of the ends off of words.

```python
not_stemmed_words = ["organize", "organizes", "organizing"]
stemmed_words = ["organ", "organ", "organ"]
```

### Lemmatization VS Stemming

Stemming and Lemmatization are both **text normalization techniques** used in NLP. They are used to prepare text, words and documents for further processing.

|                 |                        **Lemmatization**                        |                      **Stemming**                     |
|:---------------:|:---------------------------------------------------------------:|:-----------------------------------------------------:|
|  **Principle**  | combines a **word reduction** and a **morphological analysis**. | is based on **word reduction** until stem is reached. |
|    **Goals**    |               find the most simple form of a word               |              find a common form of words              |
| **Differences** |   always return an existing word / most informative technique   |        much simpler but not as much informative       |
|   **Example**   |                      was, were, been --> be                     |                 informative -> inform                 |

NLP libaries mostly use the **Lemmatization** technique which is considered as far more informative and most suitable to use.

![img_2](/ds/nlp/resources/stemming-vs-lemmatization.png)

### Word Frequency

## Training a ML algorithm

### Bags of words

Machine learning algorithms take `numbers` between `0` and `1` in input and not strings. When we want our model to associate **words** or **sentences** to **topics**, we'll create an array representing all *known words*.

```python
all_words = ["Hi", "How", "are", "you", "bye", "see", "later"]
```

We'll then have another array with the same size. This array will contain `0` and `1`:
- `0` is when the word is not used.
- `1` is when the word is used.

We want to write `how are you` to feed the ML algorithm
```python
["Hi", "How", "are", "you", "bye", "see", "later"]
[  0 ,   1  ,   1  ,   1  ,   0  ,   0  ,   0    ]
```

### An example of NLP Preprocessing Pipeline

example: "Is anyone there?" 

1. **tokenize**: ["Is", "anyone", "there", "?"]
2. **lower + stem**: ["is", "anyon", "there", "?"]
3. **exclude punctuation characters**: ["is", "anyon", "there"]
4. **bag of words**: [0, 0, 0, 1, 0, 1, 0, 1] 