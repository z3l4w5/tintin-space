---
weight: 6
bookFlatSection: true
title: "6 Structuring web pages"
bookCollapseSection: true
---

# Structuring web pages

{{< hint info >}}
**This chapter covers**

- Organizing the template for better understanding and reuse
- Using layouts and partials to structure code and improve compilation speeds
- Using content types to organize templates
- Manipulating assets using Hugo Pipes
- Using templates bundled with Hugo
{{< /hint >}}

With the Go template language in Hugo, we can build templates for markup- controlled HTML pages in as much detail as needed. In this chapter, we will enable multiple types of pages, sharing template code and snippets between them (figure 6.1). We will also look at how Hugo can help with the JavaScript, images, and CSS files using Hugo Pipes. We will build our foundation to move away from the Eclectic theme and have more control over the entire website rendering using custom template code.

{{< figure src="Figure6.1.svg" title="Figure 6.1 Chapter 6 focuses on getting multiple pages to work together, sharing the right set of snippets between them, and using assets like images, CSS files, and HTML optimally." >}}
