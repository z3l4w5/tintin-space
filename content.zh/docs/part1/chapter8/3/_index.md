---
weight: 3
title: "8.3 导入主题"
date: 2022-09-12T18:26:30+08:00
draft: true
---

# 8.3 导入主题

启用Hugo模块后，我们可以返回config.yaml对其进行管理。 如果主题作为GitHub上的Git储存库可用(就像大多数Hugo主题的情况一样)， Hugo可以自动为我们获取和设置它。 我们将试水，首先通过Hugo模块导入折衷，然后移动到AcmeTheme之后。 与从GitHub手动下载主题并将其放置在主题文件夹中不同， 我们可以在主题配置设置中放置githorb.com/hugoinaction/ecectic，如清单8.2所示，Hugo将为我们进行下载。

{{< hint info >}}
**NOTE** 如果你是离线工作，请阅读第8.7节，在那里我们将回到本地使用主题，讨论如何为其它依赖项实现这一目标。
{{< /hint >}}

{{< details title="Listing 8.2  Adding a theme via Hugo Modules" open=true >}}
```
theme: github.com/hugoinaction/Eclectic
```
{{< /details >}}

就这样。 下次我们运行hugo server或推送到GitHub页面或Netlify时，Hugo会自动从internet获取折衷主题，并使用它来渲染我们的网站。 当我们在链接到GitHub存储库之后运行Hugo服务器时，会发生许多事情(参见图8.3)：
-在后台，Hugo找出并安装了正确版本的依赖项。 Hugo还将其缓存到本地，以供后续运行。
-使用网站上的直接依赖项列表更新了go.mo d文件。
-创建了一个名为go.sum的新文件，确保Hugo将获取go.mod文件中指定的依赖项的正确版本。 就像Ruby中的Gemfile.lock和Node.js世界中的package-lock.json一样，该文件通过列出所有直接和间接依赖项的精确版本来确保构建的一致性和可重复性。

![Figure8.3](Figure8.3.svg)

图8.3当我们使用基于Hugo模块的主题加载Hugo开发服务器时，启动时发生的活动

你可以将AcmeTheme文件夹推送到新的GitHub存储库，并将其用作加载主题的位置。 你不需要将AcmeTheme存储库初始化为新的Hugo模块，也不需要添加任何代码来使用它。 如果你在配置文件config/_default/config.yaml中指定依赖项作为主题，则Hugo没有其它需要。 主题可以有一个go.mod文件来指定它的依赖项，但这不是必需的。 如果存在这样的文件，Hugo将兑现。 如果不存在这样的文件，Hugo将阅读主题。

{{< hint info >}}
**CODE CHECKPOINT**    https://chapter-08-01.hugoinaction.com, and source code: https://github.com/hugoinaction/hugoinaction/tree/chapter-08-01.
{{< /hint >}}