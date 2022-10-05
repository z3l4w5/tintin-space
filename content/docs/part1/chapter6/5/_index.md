---
weight: 5
title: "6.5 Using bundled templates for common work"
date: 2022-09-12T18:26:30+08:00
draft: true
---

# 6.5 Using bundled templates for common work

From the perspective of maintenance, the best piece of code is an empty file. The sec- ond best is a well-written piece of code maintained by a trusted team of experts. Hugo comes bundled with ready-to-use templates supported by its core team and used in hundreds of themes by the community. Reusing some of this makes life as a developer a lot easier.

When we added the head section of the website, we did not provide much meta- data. While metadata does not change the raw contents of the web page visible to the user, that information is vital for the discoverability of the web page. The Google search bot uses microdata to identify and list pages for a Google search. Services like Facebook and LinkedIn use OpenGraph tags to provide richer experiences to users sharing the web page on these platforms. 

With Twitter cards, we can control how our web page looks if someone tweets the URL.

Although we can create the metadata tags manually, there is no real need to do so. Unless we need to pass specific data to any of these tags, we can use Hugo’s internal templates for this task. These templates use the front matter, the summary, the site configuration, and the page bundle resources to generate HTML tags that we can place on our website. There is not a lot of wiggle room in the specification provided by these services. Therefore, it makes little sense to modify these. Hugo comes bun- dled with standard scripts from Google Analytics to disqus.com comments, and these can be added to the template using a single line of code.

The following listing adds Open Graph and Twitter cards to the base template for our website via internal templates. A copy of the template is also avail- able in the chapter resources (https://github.com/hugoinaction/hugoinaction/tree/ chapter-06-resources/11). The generated HTML content should have og:title and og: description along with twitter:title and twitter:description tags.

{{< details title="Listing 6.39 Adding metadata (layouts/modern/baseof.html)" open=true >}}
```
{{ template "_internal/twitter_cards.html" . }}
{{ template "_internal/opengraph.html" . }}
```
{{< /details >}}

{{< hint info >}}
**CODE CHECKPOINT**	https://chapter-06-23.hugoinaction.com, and source code: https://github.com/hugoinaction/hugoinaction/tree/chapter-06-23.
{{< /hint >}}

Just like bundled templates, Hugo provides variables and functions to reduce work. One such example is automatic summarization we introduced in chapter 4. We can access the page summary by using .Summary in the page context. Another such method is .TableOfContents, which parses the headings in the Markdown document and provides a table of contents based on that. We can configure the table of contents in the global configuration. The following listing moves the definition of the body for single pages to single.html and adds a table of contents (see figure 6.7).

{{< details title="Listing 6.40  Table of contents in single pages (layouts/modern/single.html)" open=true >}}
```html
{{define "body"}}
<main>
{{with .Title}}
<h1>
{{.}}
</h1>
{{end}}
{{if .Param "toc"}}
<h2>Table of Contents</h2>
{{.TableOfContents}}
{{end}}
{{.Content}}
</main>
{{end}}
```
{{< /details >}}

Let’s enable the table of contents for the Terms of Use page by passing toc:true in the front matter. We can also move the title from the Markdown \<h1> heading to the Title attribute in the front matter.

{{< hint info >}}
**CODE CHECKPOINT**	https://chapter-06-24.hugoinaction.com, and source code: https://github.com/hugoinaction/hugoinaction/tree/chapter-06-24.
{{< /hint >}}

{{< figure src="Figure6.7.svg" title="Figure 6.7 Table of con- tents for the Terms of Use page is enabled by using the {{.TableOfContents}} method." >}}

With the power of partials, Hugo Pipes, and bundled templates, we enhanced the index.html page and laid down the foundations of a new theme for the entire website. We can transfer any page to the new template by specifying its type as modern. In the next chapter, we will be moving away from the Eclectic theme to a custom theme called Acme that will power the Acme Corporation website.