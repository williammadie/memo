# HTML

## Table of Contents

- [What is HTML?](#what-is-html)
- [Good Practices](#good-practices)
    - [Figure or not figure](#figure-or-not-figure)

## What is HTML?

## Good Practices

### Figure or not figure

In HTML, there are **2 ways** to add images:

```html
<img src="path/img.png" alt="img description">
```

```html
<figure>
    <img src="path/img.png" alt="img description">
    <figcaption>Here is the image caption</figcaption>  <!-- Optional -->
</figure>
```

The `<figure>` tag main usage is to allow the machine to differentiate *paragraphs* and *image captions*.

