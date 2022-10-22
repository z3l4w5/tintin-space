---
weight: 6
title: "1.6 Selecting the builder"
date: 2022-09-12T18:26:30+08:00
draft: true
---

# 1.6 Selecting the builder

The Jamstack does not prescribe a specific technology. The developer is free to choose the technology of their liking to build the website. There is an extensive list of static site builders with various tradeoffs. These are made in different programming languages, provide integrations, and support many plugins.

Jekyll, built in Ruby, is a popular static site builder that seamlessly integrates with GitHub Pages. GitHub can automatically deploy Jekyll-based websites from a repository without writing a custom build step. Many Hugo users started their journeys with Jekyll and moved to Hugo looking for better build performance.

Hugo is among the fastest static site generators with a deep feature set. Hugo’s development team has focused on building a system that can render a complicated website with hundreds of pages in less than a second. Written in Go (Golang), Hugo comes as a single binary with all batteries included. With no plugins, the core team has standardized most of its features. This standardization allows building the elements with a lot of thought focusing on maintainability and performance. Its template language is a complete programming language that we can use to create anything. The documentation is well maintained, and the community is active in the forums. Many popular websites with millions of monthly users have Hugo as their generator. The core of Hugo is stable, and while it does rapidly evolve, it has compatibility with the older versions.

There is a crop of popular JavaScript framework-based static site builders like Gatsby, Nuxt, and Next.js. These force you to follow their choices of how to write and use JavaScript. Frameworks like Next.js include features to build the API backend. If you are looking to develop a JavaScript-heavy application and agree with the decisions made by these frameworks, these might be great choices. Due to the nature of the JavaScript ecosystem, and the relatively small amount of time these frameworks have been in existence, expect some churn.

There is another set of static site builders like Pelican in Python and mdBook in Rust. These are much smaller in feature sets and popularity. Use these if you are tied to a language and want to write custom features.