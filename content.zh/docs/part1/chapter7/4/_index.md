---
weight: 4
title: "7.4 创造我们自己的主题"
date: 2022-09-12T18:26:30+08:00
draft: true
---

# 7.4 创造我们自己的主题

现在我们已经将主题的重要部分移到了modern布局上，    我们不再需要兼收并蓄。我们可以安全地将其从代码库中删除，并将所有页面移到我们的定制主题中。

## 7.4.1 移至新主题
要移动到自定义主题，我们需要确保不使用折衷中的任何功能。 我们不希望在我们的新主题中需要更多工作的破碎页面。 请注意，我们不需要复制所有折衷的特征。 只需专注于我们需要的内容，然后决定我们可以删除的内容。 为了进行验证，我们将在网站的索引页面上将cascading类型开关添加到modern的内容类型中，如以下列表所示。

{{< details title="Listing 7.20  Moving all pages to content type modern (content/_index.md)" open=true >}}
```yaml
cascade:  
  type: modern
```    
{{< /details >}}

{{< hint warning >}}
**NOTE** 我们还可以使用Hugo配置来提供顶级的级联属性。 这使我们可以将此配置保留在内容之外。
通过此更改，我们将内容类型现代应用于网站上的所有页面。 我们可以验证没有主题的网站看起来不错。 注意，有一些像data-driven.md这样的破碎页面，因为我们没有添加对使用它的重要键来创建某些元素的支持。 我们不需要Acme Corporation网站中的此页面，因此我们可以从config/_default/config.yaml中删除主题/折衷文件夹和主题: 折衷设置。
{{< /hint >}}

{{< hint info >}}
**CODE CHECKPOINT**    https://chapter-07-11.hugoinaction.com, and source code: https://github.com/hugoinaction/hugoinaction/tree/chapter-07-11.
{{< /hint >}}

下一步是将布局移动到不同的主题。 雨果的主题概念是流动的。 网站可以挑选模板内容的一部分，并将其移动到主题中。 要创建一个新主题，我们需要在主题文件夹中创建一个带有主题名称的子文件夹。 我们可以选择将主题命名为任何我们想要的名称。 对于这本书，我们选择了AcmeTheme作为主题名称。 我们可以将Layout文件夹移动到Themes/AcmeTheme文件夹，以将布局作为主题的一部分进行推广。 接下来，我们需要更新配置文件中的主题，config/_default/config.yaml。 下面的清单更新了主题。

{{< details title="Listing 7.21  Setting the theme to AcmeTheme (config/_default/config.yaml)" open=true >}}
```yaml
theme: AcmeTheme
```
{{< /details >}}  	

{{< hint info >}}
**CODE CHECKPOINT**    https://chapter-07-12.hugoinaction.com, and source code: https://github.com/hugoinaction/hugoinaction/tree/chapter-07-12.
{{< /hint >}}

如果我们运行清单7.21中的代码，我们应该得到与使用我们的现代类型构建的所有页面相同的网站。 然后，我们可以通过从Themes文件夹中删除它来完全消除Eclectic主题。

## 7.4.2 将内容与主题对齐

从技术上讲，我们现在有了一个主题。 内容类型 (或迄今为止我们已覆盖的主题的任何其他部分) 与主题之间的显着概念差异是，我们构建了一个主题，以便在多个网站上重用。 但现在，它与内容结构紧密结合在一起。 如果我们在第4章 (使用代码检查点第04-11章) 之后选择了该项目，并将其主题与我们现在拥有的主题交换了，那么什么都不会起作用。 我们需要提供有意义的默认设置，并让人们很容易地拿起一个基本的雨果项目的主题。 可以通过配置，前置文件或硬编码文件位置 (例如background.svg) 访问所有添加的功能， 但基本功能应该随时可用。

第一步是删除内容类型的要求。 为此，我们需要将Themes/AcmeTheme/Layout/Modem重命名为Themes/AcmeTheme/Layout/_Default，这将使我们的布局成为默认布局。 我们拥有的代码应该继续工作，即使它引用了modern的内容类型。 在没有内容类型的情况下，Hugo会回退到默认的内容类型。 现在，我们可以从代码库中完全删除type: modern。

{{< hint info >}}
**CODE CHECKPOINT**    https://chapter-07-13.hugoinaction.com, and source code: https://github.com/hugoinaction/hugoinaction/tree/chapter-07-13.
{{< /hint >}}

我们将博客页面移至名为博客的新布局。 雨果的布局存在可发现性问题。 除非有人知道，否则找不到布局的可能性很高。 对于博客来说，作为一种新的内容类型更有意义。 因此，我们将创建一个名为themes/AcmeTheme/layouts/blog的新文件夹，并将themes/AcmeTheme/layouts/_default/blog.html移动到themes/AcmeTheme/layouts/blog/single.html。 这样，博客文件夹中的所有页面都会自动选择内容类型为博客的页面，并使用single.html模板。

很高兴看到博客页面自动获取此信息。 如果缺少特定布局，则Hugo会回退到该文件的默认布局。 由于blog文件夹中存在单个布局，因此该文件夹中的条目会自动选择该布局。 有了这一点，我们可以删除博客页面前面的布局更改。

{{< hint info >}}
**CODE CHECKPOINT**    https://chapter-07-14.hugoinaction.com, and source code: https://github.com/hugoinaction/hugoinaction/tree/chapter-07-14.
{{< /hint >}}

当我们创建博客内容类型时，博客的single.html模板会自动从 _default类型中提取基本模板 (baseof.html)。 如果基本模板不存在于特定的内容类型中，则即使是基本模板也可以退回到默认类型。 默认内容类型在Hugo中是唯一的，因为它可以为所有内容类型提供基础模板。 因此，大多数默认基本模板都是通用的和可扩展的。 我们需要在同一个网站上完全独立的HTML页面是零星的。 如果我们覆盖主题中的默认内容类型，则主题的其余部分很难正常运行。

## 7.4.3 提供主题资产

主题中定义的模板指的是Assets文件夹中的多个资产，如css文件和图像。 我们需要将这些移动到主题/AcmeTheme文件夹中，以使主题独立。 虽然移动css文件不是一个大问题，但是徽标和ducts.csv文件信息是特定于Acme Corporation网站的，不属于主题。 我们可以将空的products.csv和占位符图像放在主题文件夹中，以允许网站编译和执行 (https://github .com/hugoinaction/tree/chapter-07-resources/07)。 一旦我们移动了css文件并提供了主题资产，主题就应该独立存在了。

{{< hint info >}}
**CODE CHECKPOINT**    https://chapter-07-15.hugoinaction.com, and source code: https://github.com/hugoinaction/hugoinaction/tree/chapter-07-15.
{{< /hint >}}

{{< hint warning >}}
**NOTE** 你需要在配置中将主题名称更改为Acme才能选择此主题。
{{< /hint >}}

为了检查这一点，我们可以移动第4章中的源代码(内容和配置文件夹)，清空Assets和Archetypes文件夹，然后测试。

{{< hint info >}}
**CODE CHECKPOINT**	https://chapter-07-16.hugoinaction.com, and source code: https://github.com/hugoinaction/hugoinaction/tree/chapter-07-16. (reverted in chapter-07-17)
{{< /hint >}}

我们刚刚创建的主题可以在我们的网站之外使用。 我们现在可以将它独立地托管在它自己的单独存储库中，或者以文件夹的形式提供给其他网站集成。 我们也可以将这个主题提交给雨果主题画廊。

{{< hint warning >}}
**NOTE** Not all Hugo websites create independent themes. If you are building a theme just for your website, keeping it in this state in the themes folder may be the best approach.
{{< /hint >}}

在网站中嵌入主题可以提供最大的易用性，因为你只需管理一个代码库； 你只需要迎合单个网站的内容，而不是多个通用用例。 然后，你可以获得主题的所有灵活性，而无需为你的代码增加多个存储库的开销。

所有主题不需要公开分享。 你可以在一个组织内使用具有相同共享主题的多个网站。 销售团队可以让他们的独立网站带有内容文件夹，而文档团队也可以建立一个单独的网站。 他们都可以共享一个由工程团队管理的定制主题。

{{< figure src="Figure7.8.svg" title="图7.8删除数据: 可重复使用的主题使某些工作 (例如仅共享网站的一部分) 变得简单。 亚历克斯说服营销团队尝试这种轻量级的方法。" >}}