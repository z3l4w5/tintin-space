---
weight: 4
title: "8.4 启用Eclectic主义以外的主题"
date: 2022-09-12T18:26:30+08:00
draft: true
---

# 8.4 启用Eclectic以外的主题

向Hugo网站添加主题就像替换config.yaml中的URL一样简单，但这可能并不总是有效。 主题切换可能会失败，原因有几个：

- 某些主题需要配置中的唯一设置才能使用。
- 该网站可能依赖于在不同主题中不可用的短码。 如果缺少短代码，Hugo将无法编译。

主题导致了第一个原因，而内容创作者可能在不知不觉中导致了第二个原因。 当我们将layouts文件夹移动到AcmeTheme时，我们还移动了我们网站所依赖的短代码。 尽管这些短码有兼收并蓄的版本，但它们并没有出现在环球等其他主题中。 因此，如果你在检查站08-1获取源代码，并试图用你在雨果主题展示中找到的任何其他主题替换该主题，它将无法构建。

为了保持内容独立于主题，我们需要有一个在网站上使用的所有短码的副本，捆绑在其代码库或加载的模块(我们将在8.10节做这一点)。 为了允许其他主题，我们将在核心网站中保留部分和短代码文件夹的副本。 将这两个文件夹从Themes/AcmeTheme/Layout文件夹复制到顶级Layout文件夹。 然后，你可以通过在配置的主题部分中提供主题的GitHub路径 (例如github .com/hugo无所作为/Universal) 来使用不同的主题 (如Universal)。 请注意，因为我们去掉了主页，并且没有在Universal中配置主页，所以主页在这一点上将主要是空白的。

{{< hint info >}}
**CODE CHECKPOINT**    https://chapter-08-02.hugoinaction.com, and source code: https://github.com/hugoinaction/hugoinaction/tree/chapter-08-02.
{{< /hint >}}