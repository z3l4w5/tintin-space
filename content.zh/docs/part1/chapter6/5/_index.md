---
weight: 5
title: "6.5 将捆绑模板用于常见工作"
date: 2022-09-12T18:26:30+08:00
draft: true
---

# 6.5 使用捆绑模板进行常见工作

从维护的角度来看，最好的代码是一个空文件。 第二好的是由值得信赖的专家团队编写维护良好的代码。 Hugo与其核心团队支持的现成模板捆绑在一起，并被社区用于数百个主题。 重复使用其中的一些会使开发人员的工作轻松许多。

当我们添加网站的head部分时，我们没有提供太多的元数据。 虽然元数据不会改变用户可见的网页的原始内容，但这些信息对网页的可发现性至关重要。 Google搜索机器人使用微数据来识别和列出Google搜索的页面。 Facebook和LinkedIn等服务使用OpenGraph标签为在这些平台上分享网页的用户提供更丰富的体验。 

使用Twitter卡片，如果有人在推特上发布URL，我们可以控制网页的外观。

虽然我们可以手动创建元数据标记，但实际上并不需要这样做。 除非我们需要将特定数据传递给这些标签中的某一个，否则我们可以使用Hugo的内部模板来完成此任务。 这些模板使用front matter、摘要（summary）、站点配置和页面bundle资源来生成我们可以放置在网站上的HTML标记。 这些服务提供的规范都是固定的。 因此，修改这些规则没有多大意义。 Hugo带有Google Analytics 需要的disqus.com注释标准脚本，可以使用一行代码将其添加到模板中。

下面的清单通过内部模板将Open Graph和Twitter卡片添加到我们网站的基本模板中。 该模板的副本也可在章节资源 (https://github.com/hugoinaction/hugoinaction/tree/chapter-06-resources/11)中使用。 生成的HTML内容应该有og:title和og:description，以及twitter:title和twitter:description标记。

{{< details title="Listing 6.39 Adding metadata (layouts/modern/baseof.html)" open=true >}}
```
{{ template "_internal/twitter_cards.html" . }}
{{ template "_internal/opengraph.html" . }}
```
{{< /details >}}

{{< hint info >}}
**CODE CHECKPOINT**	https://chapter-06-23.hugoinaction.com, and source code: https://github.com/hugoinaction/hugoinaction/tree/chapter-06-23.
{{< /hint >}}

作为绑定模板，Hugo提供了变量和函数来减少工作。 我们在第4章中介绍的自动摘要就是这样一个例子。 我们可以通过使用页面上下文中的.Summary。 另一种这样的方法是.TableOfContents，它解析Markdown文档中的标题并基于此提供目录。 我们可以在全局配置中配置目录。 下面的清单将单个页面的正文定义移动到single.html，并添加一个目录(参见图6.7)。

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

让我们通过在前面的内容中传递toc:true来启用使用条款页面的目录。 我们还可以将标题从Markdown\<h1>标题移到前面内容中的标题属性。

{{< hint info >}}
**CODE CHECKPOINT**	https://chapter-06-24.hugoinaction.com, and source code: https://github.com/hugoinaction/hugoinaction/tree/chapter-06-24.
{{< /hint >}}

{{< figure src="Figure6.7.svg" title="图6.7使用 {{.TableOfContents}} 方法启用了 “使用条款” 页的目录。" >}}

利用partials、Hugo管道和绑定模板的能力， 我们增强了index.html页面，并为整个网站奠定了新主题的基础。 通过将页面类型指定为modern，我们可以将任何页面转移到新模板。 在下一章中，我们将从Eclectic主题转向称为Acme的自定义主题，该主题将为Acme Corporation网站提供动力。