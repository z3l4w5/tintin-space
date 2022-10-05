---
title: "Summary"
date: 2022-09-12T18:26:30+08:00
draft: true
---

# Summary

Hugo Modules is a powerful way to manage dependencies. We can mount any folder in any Git repository at any location in our project, even if the source repository knows nothing about Hugo or Hugo Modules.

Hugo provides the means to manage dependencies in whatever approach we desire. We can keep dependencies in the vendor folder, download them on the fly from a link, or have a local copy on disk.

We can use Hugo Modules to create themes, template plugins, and content plugins. These plugins can mount to any location in a Hugo repository and have access to the entire template language. We can override specific files in a plugin for customization.

Modules can depend on other modules, and we can decide to use the depen- dencies directly.

Hugo makes it easy to deduplicate and have one copy of a module.
