---
layout: post
title: Sample Post
excerpt: "Just about everything you'll need to style in the markdown-article: headings, paragraphs, blockquotes, tables, code blocks, and more."
modified: 2016-07-11T14:17:25-04:00
categories: articles
tags: [markdown]
author: hush_please
image:
  feature: so-simple-sample-image-1.jpg
  credit: WeGraphics
  creditlink: http://wegraphics.net/downloads/free-ultimate-blurred-background-pack/
comments: true
share: true
---

Below is just about everything you'll need to write your markdown-articles. Check the source code to see the many embedded elements within paragraphs.

# Heading 1

## Heading 2

### Heading 3

#### Heading 4

##### Heading 5

###### Heading 6

### What is [software engineering](https://en.wikipedia.org/wiki/Software_engineering)?

As software engineers, we use our knowledge of computers and computing to help solve problems. **Often the problem** with which we are dealing is related to a computer or an existing computer system, but sometimes the difficulties underlying the problem have nothing to do with computers.

![Smithsonian Image]({{ site.url }}/images/3953273590_704e3899d5_m.jpg)
{: .pull-right}

*Therefore, it is essential that we first understand the nature of the problem.* In particular, we must be very careful not to impose computing machinery or techniques on every problem that comes our way. We must solve the problem first. Then, if need be, we can use <cite>technology</cite> as a <u>tool</u> to implement our solution. 
HTML and <abbr title="cascading stylesheets">CSS<abbr> are our tools. 

### Blockquotes

> Software engineering is the application of engineering to the design, development, implementation, testing and maintenance of software in a systematic method.

## List Types

### Ordered Lists

1. Item one
   1. sub item one
   2. sub item two
   3. sub item three
2. Item two

### Unordered Lists

* Item one
* Item two
* Item three

## Tables

| Header1 | Header2 | Header3 |
|:--------|:-------:|--------:|
| cell1   | cell2   | cell3   |
| cell4   | cell5   | cell6   |
|----
| cell1   | cell2   | cell3   |
| cell4   | cell5   | cell6   |
|=====
| Foot1   | Foot2   | Foot3   |
{: .table}

## Code Snippets

Syntax highlighting via Rouge

```css
#container {
  float: left;
  margin: 0 -240px 0 0;
  width: 100%;
}
```

Non Rouge code example

    <div id="awesome">
        <p>This is great isn't it?</p>
    </div>

## Buttons

Make any link standout more when applying the `.btn` class.

<div markdown="0"><a href="#" class="btn">This is a button</a></div>
