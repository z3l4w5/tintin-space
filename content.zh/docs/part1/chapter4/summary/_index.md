---
title: "总结"
date: 2022-09-12T18:26:30+08:00
draft: true
---

# 总结

Hugo提供了覆盖全局配置变量的灵活性，并通过多个文件和在各种环境中管理它们。 通过将配置从单个文件移动到文件夹，我们可以根据多种条件选择选项。

我们可以通过将相应的标记内容放入文件夹来将Hugo中的网页组织成各个部分。 这些部分可以嵌套，通常与网站的URL方案相匹配。

我们可以使用各个sections的索引页面来访问内容，并将这些页面添加到菜单中。

为了实现内容跨网站的可移植性，Hugo提供了拥有独立和隔离数据的能力。 我们可以通过在前面放置菜单项并使用页面包来实现这种隔离。

使用leaf和branch bundle，我们使所有assets更接近内容。 我们可以将特定于页面的图像和文件捆绑在与页面的标记内容相同的文件夹中。

Hugo提供了通过taxonomies以任何所需的方式逻辑组织内容的能力。 每个Taxonomy都由项组成，并且一个页面可以存在于多个Taxonomy中，并且具有许多项。

分类创建列表页，并支持页面和分类术语之间的多对多映射。 我们可以根据需要定义尽可能多的Taxonomy。

Shortcode是一种提供代码片段的方法，我们可以使用这些代码片段来扩展MarkDown的新功能。 Hugo捆绑了各种用例的Shortcode，从YouTube视频到语法highlighting显示。

我们可以定义标记和HTML格式的自定义Shortcode，并与内容保持一致，以避免复制和粘贴呈现逻辑的需要。