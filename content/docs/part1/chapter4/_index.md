---
weight: 4
bookFlatSection: true
title: "4 Content management with Hugo"
bookToc: false
bookCollapseSection: true
---

# Content management with Hugo

{{< hint info >}}
**This chapter covers**
- Organizing pages into sections and menus in a Hugo website
- Grouping related content using Hugo taxonomies
- Bundling page contents into a page bundle
- Using Hugo’s built-in and community-provided shortcodes for more Markdown features
- {{< /hint >}}

A website is not just a bundle of web pages scattered at random URL locations. The pages need to be discoverable, organized into  meaningful  sections,  and  there  needs to be a way to navigate to them for a reader to be successful. Content in most websites is laid out with a strategy; grouped, tagged, and navigation cues are pres- ent in pages for the reader to navigate to others.

There are two distinct roles in a website’s development team: the content owner and the theme developer. The content owner decides the content that shows up on  the website, and the theme developer focuses on surfacing content. In this chapter, we
will be playing the role of the content owner (also called author or website editor) for the Acme Corporation website.

We will look into content organization and management in this chapter (see figure 4.1). In section 4.1, we will organize the configuration in the config folder. In sections
4.2 to 4.4, we will discuss the means to manage and associate content on a Hugo web- site. Section 4.5 will go into shortcodes, which live in the layouts folder. Shortcodes pro- vide the means to extend Markdown and share content between different pages in Hugo.

![Figure4.1](Figure4.1.svg)

Figure 4.1 The author and the developer organize the website’s contents into files and folders that are then stored in the content directory. This chapter focuses on the organization of the content directory for optimal resource management. We will also organize the configurations in the config folder and will create shortcodes in the layouts folder to extend Markdown.
