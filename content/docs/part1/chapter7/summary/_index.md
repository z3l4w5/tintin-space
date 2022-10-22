---
title: "Summary"
date: 2022-09-12T18:26:30+08:00
draft: true
---

# Summary

We can use layouts to order different content within the same content type.

The cascade option in the front matter allows us to share front matter properties with all pages in a branch bundle.

The templates single.html and list.html are essential in completing a Hugo theme. They correspond to leaf bundles (or individual pages) and branch bundles, respectively.

The index.html, taxonomy.html, and terms.html files default to list.html if any of those files are not present.

The files taxonomy.html and terms.html provide fine-grain control over the website taxonomy.

A Hugo theme is a collection of templates, shortcodes, assets, and other resources to render a website when provided in the content folder.

As template authors, we should aim to create a template that can render with an arbitrary content folder. All features should be opt-in and provide sensible defaults.

Content views are subtemplates that render in another template. They act as more flexible replacements for partials, which override content types.
