# HTML

## Table of Contents

- [What is HTML?](#what-is-html)
- [Arrays](#arrays)
- [Media Queries](#media-queries)
- [Good Practices](#good-practices)
    - [Figure or not figure](#figure-or-not-figure)

## What is HTML?

## Arrays

Create a simple Array
```html
<table>
   <caption>Title of my Array</caption>

   <tr>
       <th>Column1Header</th>
       <th>Column2Header</th>
       <th>Column3Header</th>
   </tr>
   <tr>
       <td>Value(0:0)</td>
       <td>Value(0:1)</td>
       <td>Value(0:2)</td>
   </tr>
   <tr>
       <td>Value(1:0)</td>
       <td>Value(1:1)</td>
       <td>Value(1:2)</td>
   </tr>
</table>
```

Move the Title
```css 
caption-side: top;
caption-side: bottom;
```

Create a complex Array
```html
<table>
    <caption>Title</caption>

    <thead>     <!-- Header -->
        <tr>
            <th>Column1Header</th>
            <th>Column2Header</th>
            <th>Column3Header</th>
        </tr>
   </thead>

   <tfoot>      <!-- Foot -->
        <tr>
            <th>Column1Header</th>
            <th>Column2Header</th>
            <th>Column3Header</th>
        </tr>
   </tfoot>

   <tbody>
        <tr>
            <td>Value(0:0)</td>
            <td>Value(0:1)</td>
            <td>Value(0:2)</td>
        </tr>
        <tr>
            <td>Value(1:0)</td>
            <td>Value(1:1)</td>
            <td>Value(1:2)</td>
        </tr>
    </tbody>
</table>
```

Merge cells horizontally
```html
<tr>
    <td>Value(1:0)</td>
    <td colspan="2">Value(1:1)</td>
</tr>
```

Merge cells vertically
```html
<tr>
    <th>Pour enfants ?</th>
    <td>Non, trop violent</td>
    <td>Oui, adapté</td>
    <td rowspan="2">Pour toute la famille !</td>
</tr>
<tr>
    <th>Pour adolescents ?</th>
    <td>Oui</td>
    <td>Pas assez violent...</td>
</tr>
```

## Media Queries

### Things to know

- It is possible to specify new CSS stylesheets for screen with given resolution. It helps to keep things clear. This file will be load only if necessary. Keep in mind that it is not always possible (for instance when you use Angular)

### Write Media Queries

For screens with a maximal width of 1280px
```css
@media screen and (max-width: 1280px) {
    /* Specify CSS properties here*/
}
```

For all screen types with a minimal width of 1024px and a maximal width of 1280px
```css
@media all and (min-width: 1024px) and (max-width: 1280px) {
    /* Specify CSS properties here*/
}
```

For all TV screens
```css
@media tv {
    /* Specify CSS properties here*/
}
```

For all vertically oriented screens
```css
@media all and (orientation: portrait) {
    /* Specify CSS properties here*/
}
```

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

## Limits

- It is not possible to modify a tag that is not linked to another tag with CSS only. If you want to do something like this, you'll have to use JavaScript.