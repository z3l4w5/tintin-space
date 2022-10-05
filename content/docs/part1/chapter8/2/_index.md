---
weight: 2
title: "8.2 Themes as Hugo Modules"
date: 2022-09-12T18:26:30+08:00
draft: true
---

# 8.2 Themes as Hugo Modules

Themes are the most common shared element across multiple websites. They are the most common use case for Hugo Modules. In section 2.2, where we introduced the concept of themes, we discussed three ways to integrate themes into a website: down- load and copy (which we have used so far), Git submodules (not recommended any- more), and Hugo Modules (which we did not use because download and copy is easier for beginners). We used download and copy because it is easy to get started with, but it has some downsides:

- Updates—Distributing a theme’s updates is painful. Everyone keeps a copy of  the theme. Updating is a manual operation as you need to download a new ver- sion. There is no intuitive way to know of a new release, and developers are free to modify their local copies, making updates even harder.
- Dependencies—Although we hardcoded all our CSS and JavaScript files in the AcmeTheme module so far, it is rare to have an independent website. Chances are high that a theme might depend on a JavaScript or CSS library maintained elsewhere. If that library is downloaded and copied into the theme, then updat- ing is also manual.
- Size and sharing—Keeping a copy of the theme bloats the size of our code reposi- tory. Sharing an enormous repository can be clunky. The code present in the theme can also botch a reporting build. Automated tools that modify the codebase can mess up with bundled themes, causing confusion and a waste of resources.

These problems are primarily caused by copying the theme’s source code rather than linking to it. Linking is a much cleaner solution than downloading and copying. If we need a backup of a repository, a linked fork (copy of a Git repository that can have links to the original code) or an external archive is a much better idea than a bundled copy of the resource. That way, we make it easy to get dependencies and also to share the theme across websites.