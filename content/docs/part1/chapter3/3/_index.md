---
weight: 3
title: "3.3 Other markup languages"
date: 2022-09-12T18:26:30+08:00
draft: true
---

# 3.3 Other markup languages

Hugo natively supports Markdown and HTML for content markup. The parsers for these languages are written in Go and are embedded in Hugo, receiving the love and care from the Hugo team to ensure outstanding performance. Hugo also supports AsciiDoc, pandoc, and reStructuredText for providing content. These languages are not available natively in Hugo but instead are supported via external helpers. External helpers are software programs that Hugo calls over the command line to get some content parsed. Because they are outside Hugo, Hugo cannot guarantee their perfor- mance. Table 3.1 compares the different markup languages supported by Hugo.

Table 3.1 Content markup languages in Hugo

- Markdown trades simplicity and ease of use over features. It is the perfect lan- guage for website content that does not span beyond a couple of pages. Hugo’s Markdown parser is fast and powerful. For users new to Hugo, it is recom- mended to begin with the Markdown format unless they already know a differ- ent markup language.
- HTML (HyperText Markup Language) is also a markup language. Because this is the format that web browsers understand, no translation is needed when we provide content in this language. HTML is more human-readable in its native form than a format like DOC or PDF, and it offers more power than most other markup languages. We can write HTML directly in Hugo and still take advan- tage of Hugo’s template features that we will discuss in the upcoming chapters. Writing plain HTML does come at a disadvantage, though. While writing basic HTML, we tend to mix up the page layouts and structure with content. Languages like Markdown force us to focus on content, but a strict disciplinarian can eke out better performance by using plain HTML with Hugo.
- AsciiDoc focuses on documents with hundreds of pages and is the most popular  of the markup languages among book authors. It provides more features than Markdown, although that comes at the cost of not supporting many program- ming languages and frameworks. The source code for this book is in AsciiDoc.
- pandoc is a file format converter that supports a superset of Markdown, which Hugo can convert to HTML using its command line.
- reStructuredText focuses on generating documentation projects. It is formally defined and has a stricter language providing easier parsing at the cost of simplicity.

Note that Hugo constantly adds support for new formats. As of writing this book, there were active discussions to support AsciiDoc in Hugo natively. With native support, AsciiDoc would get a performance boost, and we will have an option for choosing that language for content with minimal downsides.