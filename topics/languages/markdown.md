# Markdown

## Overview

[Markdown](https://en.wikipedia.org/wiki/Markdown) is (ironically) a markup language that simplifies creating formatted text. It aims to be easy to read in both formatted and plaintext versions. It is highly useful when creating easy to read documents that have hyperlinks and references, like these notes!

## Syntax

**Note**: Although simple to learn, markdown syntax can be complicated to follow as there is a largely been a lack of standardization in markdown parsing engines. The past few years (July 2023 curr. date) have seen more standardization, but there are still many different variations between engines. This is mostly seen in the extended syntax as most engines support the common syntax, aka [CommonMark](https://commonmark.org/).

Common Syntax:

| Element | Syntax |
| --- | --- | 
| Headings | `#` for *h1* or `##` for *h2* |
| Bold | `**bold**` |
| Italicized | `*italicized*` |
| Ordered List | `1. one 2. two`  |
| Unordered List | `- one - two`  |
| Code | \`code\` |
| Horizontal Rule | `---` |
| Link | `[link](https://www.example.com/)` |
| Image | `![image](https://www.example.com/)` |
| Blockquote | `> blockquote here` | 

**Note**: Most engines support replacing URLs with local files on links an images. For *Links* some even support putting header names in the URL section.
> e.g. \[image\](./local/image.png)

> e.g. \[link\](#heading-name)

GFM (Github Flavored Markdown) Extended Syntax:

| Element | Syntax |
| --- | --- | 
| Strikethrough |  \~\~strikethrough\~\~ |
| Tables | \| col1 \| col2 \| ... | 
| Task List | - \[ \] or -\[x\] |

**Note**: Extended syntax is where it gets a little messy between different flavors of markdown. Refer to [this](https://gist.github.com/vimtaai/99f8c89e7d3d02a362117284684baa0f) great guide to see the syntax differences between the different flavors.

## Reference

[Markdown Guide](https://www.markdownguide.org/cheat-sheet/)

- Great cheat sheet to get started

[Markdown Flavors](https://gist.github.com/vimtaai/99f8c89e7d3d02a362117284684baa0f)

- Good guide on syntax differences between flavors.