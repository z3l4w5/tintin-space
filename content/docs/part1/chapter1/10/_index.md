---
weight: 10
title: "1.10 Cases that don’t map to Hugo"
date: 2022-09-12T18:26:30+08:00
draft: true
bookToc: false
---

# 1.10 Cases that don’t map to Hugo

Like all tools, Hugo has its use cases. Apart from all the Jamstack limitations that apply to any of the Jamstack frameworks, we need to understand that Hugo’s focus is on the markup portion of the Jamstack only. While Hugo provides the fastest available Java- Script bundler and has good support for the npm ecosystem, it takes a hands-off approach to the JavaScript and the API layers of the Jamstack. If you want to build a tool which requires a lot of JavaScript to intermingle with the static pages, or you want to have an API that shares code with the website template, Hugo’s approach of having these pieces independent falls short.

Hugo might not be optimal when we need some functionality that Hugo does not have, and we cannot achieve that with an API. Hugo keeps its core inaccessible to the templates and modules to maintain its flexibility and to keep its performance intact. Hugo is likely not the right choice for developers wanting to build a customized static site builder with lots of plugins catering to an uncommon use case. For example, if we need to interact with the SOAP or FTP protocols at compile time, that may not be pos- sible with Hugo (as of v0.91.2).