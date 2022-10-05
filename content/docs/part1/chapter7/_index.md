---
weight: 7
bookFlatSection: true
title: "7 Creating your own theme"
bookToc: false
bookCollapseSection: true
---

# 7 Creating your own theme

{{< hint info >}}
**This chapter covers**
- Creating multiple layouts with shared base templates
- Using front matter cascades in Hugo
- Creating index and taxonomy pages to navigate through the website
- Converting content type to a theme
- Building content views to share content between templates
{{< /hint >}}

In chapter 6, we started moving away from the Eclectic theme and began to create the underpinnings for a new theme. We created a new content type called modern, which has custom template code. In this chapter, we will convert the modern con- tent type to a complete theme (AcmeTheme). We will also focus on all types of con- tent and how that fits together in a new theme as figure 7.1 illustrates.

In Hugo, a theme does not have a rigid definition. A set of templates that can ren- der the content folder to a website is technically a theme. If we take the modern con- tent type that we have so far and place it in the themes/<theme name>/_default/ folder, we could call that a theme, but it would not be a good theme. It will not render the list pages (the root pages of the branch bundle) well. The taxonomy pages will also be mostly blank. A proper theme in Hugo should be able to render all the standard types of content from regular pages to list pages and taxonomy.

{{< figure src="Figure7.1.svg" title="Figure 7.1 Chapter 7 focuses on going through the breadth of the website and making sure all pages can move from the Eclectic theme to our new theme. The chapter also goes into the theme/layout split and how to get parts of the page from different areas." >}}

Currently, we depend on the Eclectic theme for a lot of pages. In this chapter, we will move the pages, one by one, to the modern content type, and once that migration is complete, we will be able to restructure that content type to become a theme.