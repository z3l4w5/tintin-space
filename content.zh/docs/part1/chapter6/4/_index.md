---
weight: 4
title: "6.4 控制Markdown渲染"
date: 2022-09-12T18:26:30+08:00
draft: true
---

# 6.4 控制Markdown渲染

我们在Markdown文档中也有图像，我们没有针对production环境进行优化。 这些也会减慢网站的加载速度。 为了控制Hugo在Markdown文档中呈现内容的方式，Hugo提供了到Markdown解析器的挂钩(称为呈现挂钩模板)，我们可以在其中定制Markdown元素的呈现。 如果需要，我们可以覆盖图像，链接甚至标题的渲染。 在优化图像时，我们将覆盖Markdown中的图像渲染功能，将图像的最大尺寸限制在1000px。 下面的清单显示了如何在modern内容类型中添加图像渲染挂钩，该类型使用resize功能 (https://github.com/hugoinaction/hugoinaction/tree/chapter-06-resources/10)。

{{< details title="Listing 6.38 Controlling image size (layouts/modern/_markup/render-image.html)" open=true >}}
![Listing6.38](Listing6.38.svg)
{{< /details >}}    	

很难直观地看到我们的Markdown挂钩是否实际执行了，因为我们没有更改图像。 我们可以查看网页的HTML源，并检查是否有延迟加载 (loading="lazy") 来验证。