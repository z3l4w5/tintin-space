---
weight: 5
title: "2.5 满足性能和可维护性的目标"
date: 2022-09-12T18:26:30+08:00
draft: true
---

# 2.5 满足性能和可维护性目标

Hugo和Jamstack承诺可靠的性能和较低的持续维护成本。 这两者本身都不是绝对的。 这里有一个梯度：我们需要在功能、开发和使用的简易性、维护和性能之间选择合适的平衡，以获得最佳效益。 没有图像的网站加载速度可能比有数百个图像的网站更快，但这并不意味着它将是所有场景的最佳网站。 因此，在分析性能和可维护性时，我们需要考虑用户场景。

## 2.5.1 性能

性能是Hugo的开发团队用来对其构建进行基准测试的一个值得注意的指标。 对于典型的场景，我们应该能够获得良好的性能，而不会遇到任何重大困难。 我们正在为Acme公司的所有网页托管在一个CDN(预渲染)，客户端不需要做太多的处理来显示网站。 虽然我们应该找到网站可以快速加载，但至关重要的是要将性能作为一个数字并在整个构建中制成表格，以便能够比较更改并修复回归。

衡量绩效的标准工具是名为LighTower(https://developers.google.com/web/tools/lighthouse/)的审核工具   它内置在谷歌的Chrome浏览器中 (图2.14)。 对于Acme Corporation，About页面代表网站的常规页面，我们将测量该页面的性能。

![Figure2.14](Figure2.14.svg)

图2.14 使用Google Chrome Lighthouse性能测试的Acme Corporation关于页面的性能审计。

{{< hint warning >}}
**NOTE** Chrome会定期使用新测试更新Lighthouse工具，因此测量结果可能与所示屏幕截图不完全一致。
{{< /hint >}}

衡量CDN上托管站点的性能至关重要，因为Hugo的开发服务器不是用户在生产中获得的。 它是为开发而建的，没有提供正确的结果。 为了衡量托管站点的性能，

- 1 转到Google Chrome中的视图 > 开发人员工具菜单以打开web检查器。
- 2 转到灯塔选项卡并运行审计。你应该能够在大多数Hugo网站上获得一个不错的审计分数。

Lighthouse可能会暗示主题中的问题。 如果是这样，则可以选择克隆主题或创建bug以供主题开发人员修复。

## 2.5.2 可维护性

web设置的可维护性很难直接衡量。 没有工具可以判断堆栈是否可维护。 检查维护系统需要花费多少精力的一种方法是列出其每个依赖项，并找出哪些依赖项需要持续的安全更新，哪些需要被开发人员放弃，或者哪些可能由于嵌套依赖项而变得难以更新。 我们还应该衡量消除依赖的效果，以防它没有得到积极的维护。 幸运的是，对于我们刚刚讨论的基于Hugo的设置，我们几乎没有依赖。 在我们的度量系统中，我们可以将重写、巨大更新或部分重写视为高风险，将不涉及太多更改的调整视为中等风险。  同时，这里的低风险是指不需要最小的人工干预。 让我们在下一次练习之后，尝试为我们到目前为止构建的网站评估这一点。

{{< hint info >}}
**Exercise 2.8**

对一个网站的性能进行基准测试的主要原因是什么？
- a. 找出整体性能问题。
- b. 绘制图表以显示在我们的网站上。
- c. 比较我们网站的多个版本和Hugo的多个版本的性能，以找出错误的行为。
- d. 在我们的网站上查找错误。
{{< /hint >}}

我们的Acme公司在本章中创建的网站依赖于Hugo。 Hugo在过去的版本中有过突破性的变化，但大多数都是轻微的。 我们不需要更新安全修复程序，因为它是仅开发的依赖。 如果我们对网站感到满意，这可能会被评为ongoing effort的较低评级，或者upgrade的中等评级。

GitHub页面上的托管不需要持续的维护。 这是互联网上对开发者最关键的服务之一。 因此，我们可以将正在进行的维护和升级的评分降低到较低水平。 如果我们使用Netlify，它会为我们管理维护，而且工作量也很低。 由于它比GitHub受欢迎程度低得多，因此存在Netlify转向新业务模型或关门的固有风险。 对于在这里建立的这种类型的网站来说，迁移到GitHub很容易，而且总体风险很低。

为Acme Corporation选择的Eclectic主题取决于一些基于JavaScript的插件。 然而，这些插件是稳定的，多年来没有发生重大变化。 尽管如此，Eclectic并没有被大量使用，如果它被放弃，Acme公司的团队将不得不承担添加修复程序的任务，以便在他们想要更新网站时支持较新的Hugo版本。 这将是一个medium effort的承诺(除非他们想要新的功能)。

总体而言，为使我们在本章中建立的网站保持活力而正在进行的工作负担很轻。  如果我们需要升级它，工作量将是低到中等的，这取决于Hugo的突破性变化和主题开发人员适应这些变化的能力。 请注意，随着本书的进一步发展，我们将在网站上添加更多依赖项，尤其是在第2部分中。 这将增加维护开销。 虽然已经尝试寻找自包含的依赖项，但建议读者在每次需要在自己的项目中添加依赖项时权衡添加依赖项的利弊。

## 2.5.3 明智地选择主题

网站的性能和维护风险在很大程度上取决于所选的主题。 如果主题不好，Hugo保持其性能的辛勤工作将不会在你的网站的构建时体现出来。 基于Hugo的网站的主要维护风险是依赖于不再与较新版本的Hugo兼容的主题的风险。 我们可以无限期地继续使用旧版本的Hugo和主题，而不必太担心安全问题，因为内容是静态的。 但是，如果我们想更新Hugo并且不再支持该主题，那么我们将独自维护该主题。 保持内容对主题不可知是一个好主意，至少在网站项目的早期是这样的，这样如果我们发现我们正在使用的主题有问题，我们可以迅速转移到不同的主题。

主题也可以成为学习如何最好地使用Hugo的绝佳来源。 许多使用Hugo的开发人员选择某个现有主题作为起点，而不是建立一个全新绝对的解决方案。 选择Hugo的一个重要原因是自定义所有内容，分支主题是任务很方便。 到第7章结束时，我们将从Eclectic的主题转移到我们的定制主题。

如果我们想继续以其他人维护的主题来构建我们的网站，那么调查可移植性是一个好主意。 Hugo提供了跨主题的标准化，切换Hugo主题并不困难(请参见清单2.8)。 我们将在Acme Corporation的网站上添加另一个主题，以确保我们的代码是可移植的。 我们在章节资源中为Hugo提供了通用主题的副本(https://github.com/hugoinaction/hugoinaction/tree/chapter-02-resources/08)  同时它也位于  github.com/hugoinaction/Universal. 你可以将该主题复制到theme文件夹，并通过网站配置启用它。 你可能需要重新启动开发服务器。

{{< details title="Listing 2.8  Changing a theme to Universal (config.yaml)" open=true >}}
```yaml
theme: Universal
```
{{< /details >}}

虽然以前的代码可以工作并呈现网站，但我们需要做更多的配置来获得通用主题的最大好处。 为此，请将logo.png放在static/image/logo.png文件夹中，并更新配置以包括以下列表中的参数 (在页脚的现有参数下方)，以便通用能够解析它们 (https://github.com/hugoinaction/hugoinaction/tree/chapter-02-resources/09)。

{{< details title="Listing 2.9  Changes to support the Universal theme (config.yaml)" open=true >}}
```yaml
theme: Universal
params: 
  footer:
  ...
  style: blue
  logo: /image/logo.png 
  logo_small: /image/logo.png 
  about_us: >
    Acme Corporation is the world's leading manufacturer of digital shapes. From squares and circles to triangles and hexagons, we have it all. Browse through our collection of various forms with different thicknesses and line styles. We shape the world.
    You live in it.

  recent_posts: 
    enable: true
```
{{< /details >}}

通用的配置文件在本书的代码资源中以TOML和YAML格式提供 (https://github.com/hugoinaction/hugoinaction/tree/ chapter-02-resources/10)。 注意，Eclectic的配置并没有被删除，我们可以很容易地在这两个主题之间切换。

{{< hint info >}}
**CODE CHECKPOINT**	https://chapter-02-05.hugoinaction.com, and source code: https://github.com/hugoinaction/hugoinaction/tree/chapter-02-05.
{{< /hint >}}

因为每个主题都有一个独特的主页，如果我们选择自己定制的基于HTML的主页，切换主题将会容易得多。 这样，如果我们现在渲染或实时重新加载，主页将保持不变。 因为About页面设置了样式，所以如果我们切换到该主题，它将匹配Universal主题(图2.15)。

![Figure2.15](Figure2.15.svg)

图2.15 Acme Corporation的“使用条款”页面，代码 (左)，Eclectic主题(中) 和Universal主题 (右)。 当我们在Hugo中切换主题时，我们提供的大部分Markdown内容仍然有效。 只需要重做配置文件之类地方提供的参数。

在这本书的其余部分，我们将回归Eclectic。 有了一个正在运行的网站，是时候添加更多的内容了，所以我们将在第3章中开始这方面的工作。