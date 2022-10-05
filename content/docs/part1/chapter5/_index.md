---
weight: 5
bookFlatSection: true
title: "5 Custom pages and customized content with the Go template language"
bookToc: false
bookCollapseSection: true
---

# 5 Custom pages and customized content with the Go template language

{{< hint info >}}
**This chapter covers**
- Customizing pages and shortcodes
- Rendering content and accessing variables and functions in the Go template language
- Accessing Hugo’s configuration and front matter in code
- Reading from the filesystem
- Creating reusable page templates called archetypes
{{< /hint >}}

One strength of Hugo is its clear separation of concerns between content (Markdown) and presentation (HTML/CSS/JavaScript). When we create content, we rarely have to deal with HTML. Team members who are not well versed in HTML or CSS can be successful with Hugo as a content management system using features we’ve discussed so far in this book. However, we can unlock a lot more power by digging deeper into layouts and HTML generation.

Chapter 2 has a section where we step out of the theme to create the home page in pure HTML. In doing so, we eschewed the role of the content creator and went into web developer mode, while primarily supplying content for the other pages. In this chapter, we will get first-hand experience with Hugo’s template language and its rendering mechanism as we improve the home page for the Acme Corporation website. In addition, we will add some features based on the content that a static HTML page cannot provide.

The pure HTML index page we currently have for the Acme Corporation website has an intermingling of content and layout. This approach has a massive set of problems:

- We cannot share parts, HTML fragments, or data between pages.
- Data and layout are interspersed in the HTML file so changing the textual content needs an understanding of HTML.
- HTML is not as easily human-readable as is Markdown and YAML.
- HTML does not have variables, conditionals, and loops, making it difficult to manage pages with a repetition of content.

Even for a single page, writing using the template logic is better than using plain HTML. We can simplify the maintainability of a website by using a template instead of simple HTML. One significant benefit of Hugo is the blurriness of the boundary between the theme and the content. Hugo provides the power to use a theme partially and override parts of web pages or to write our custom pages using all the features available to themes. In the following two chapters, we will move away from the Eclectic theme. Because we do this in a piecemeal manner, our website will still be functional the whole time.

This chapter deals with a single-page template as illustrated in figure 5.1. In section 5.1, we will split the layout and the content for the index page of the Acme Corporation website. In section 5.2, we will enhance the index page with information generated by Hugo based on the content of the rest of the website. Section 5.3 provides a glimpse of data-driven web pages built using structured front matter and data files. Finally, in section 5.4, we will use the teachings in this chapter to help our content editor by contributing as developers to provide some content automation.