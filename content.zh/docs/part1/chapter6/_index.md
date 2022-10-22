---
weight: 6
bookFlatSection: true
title: "第6章 结构化网页"
bookCollapseSection: true
---

# 第6章 结构化网页

{{< hint info >}}
**本章涵盖**

- 组织模板，以便更好地理解和重复使用
- 使用layouts和partials来构造代码并提高编译速度
- 使用content types组织模板
- 使用Hugo管道操纵assets
- 使用与Hugo打包的模板
{{< /hint >}}

使用Hugo中的Go模板语言，我们可以根据需要为标记控制的HTML页面构建模板。 在本章中，我们将启用多种类型的页面，在它们之间共享模板代码和代码片段(图6.1)。 我们还将研究Hugo如何使用Hugo Pipes帮助处理JavaScript，图像和CSS文件。 我们将建立我们的基础，以摆脱Eclectic主题，并有更多的控制整个网站渲染使用自定义模板代码。

{{< figure src="Figure6.1.svg" title="图6.1 第6章着重于使多个页面一起工作，在它们之间共享正确的代码段集，并以最佳方式使用图像，CSS文件和HTML等资产。" >}}
