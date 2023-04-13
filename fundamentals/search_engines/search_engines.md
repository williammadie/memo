# Search Engines

## Table of content

- [Indexing Pages](#indexing-pages)
- [Type of Search Engines](#type-of-search-engines)
    - [Boolean Search Engine](#boolean-search-engine)
    - [Vector Search Engine](#vector-search-engine)

## Indexing Pages

Search Engines use **indexes** which can be seen as **humongous databases containing the main topic of a website**.

It takes 3 main steps to make a **Search Engine** work:

1. Crawling: The **Search Engine** crawls the web to see what documents are available. The little spyder follows the links from one page to another. On their way, they **index** everything.
2. Indexing: Indexed pages are stored in a **gigantic database** where it can be retrieved later. It will be used by **ranking algorithms** to order results based on the user query.
3. Ranking: The user writes a request and the the indexing program coupled with the **Search Engine algorithms** are used to rank the results.

![img_1](/fundamentals/search_engines/resources/search-engine-steps.webp)

## Type of Search Engines

### Boolean Search Engine

It mainly relies on **boolean operators** as `AND, OR, NOT` and is used to do a very accurate search. 

### Vector Search Engine

In a Vector Search Engine, documents or webpages are represented by a vector. These vectors are built on a axe-system of **topics**. Each dimension is a specific topic.

![img_2](/fundamentals/search_engines/resources/vector-search-engine.png)
