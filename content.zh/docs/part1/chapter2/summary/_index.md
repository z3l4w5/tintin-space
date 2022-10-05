---
title: "总结"
---

# 总结

Hugo可以安装在Linux、MacOS和Windows上的大多数主要包管理器中。

Hugo has extensive command-line functionality to minimize the work that its users need to do. It has handy options that help build all parts of a website, from adding module dependencies to creating new Markdown-based documents.

A Hugo project consists of folders beyond the content and themes folders: static for static content, data for structured data, layouts for theme overrides, resources for Hugo’s internal caching, assets for images, JavaScript, and CSS files, and public for the generated output. It also includes archetypes for posted templates and a configuration file for global settings.

Hugo themes can be added in various ways, the simplest of which is to directly copy a theme to the themes folder. We need to configure these with standard   and theme-specific parameters and file placements before using.

Content can be added as Markdown, theme-specific structured data, or in an overridden HTML template.

Hugo websites can be hosted easily across the planet via GitHub Pages and Netlify, which provide continuous delivery support without making the devel- oper do much work.

We can switch themes, but if we use a lot of theme-specific data (like data sup- plied via params in the configuration), then that work needs to be redone. We should investigate theme switching early on so that we can switch out quickly if the Hugo theme gets abandoned.

We can use Google Chrome’s Lighthouse feature for measuring performance.

We should also do a full dependency audit to check maintainability.

Every website needs to be monitored for maintainability and performance regu- larly during development to ensure quality. Hugo offers excellent performance and has a small set of dependencies, but the website performance and main- tainability still depend on the chosen theme.