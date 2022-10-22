---
weight: 1
title: "8.1 设置Hugo模块"
date: 2022-09-12T18:26:30+08:00
draft: true
---

# 8.1 设置Hugo模块

Hugo模块依赖于围棋。 你可以使用软件包管理器或使用https://golang.org/doc/install. 中的说明安装Go 请记住，GO需要出现在系统路径中才能由Hugo使用。

要验证Go是否可用，请运行命令go version，该命令在控制台中输出Go的版本。 确保Go的版本高于1.12。 一旦我们安装了受支持的Go版本，我们就可以忘记Go并回到Hugo。 这就是我们将在整本书中用Go语言处理的所有安装。

{{< hint info >}}
**NOTE** 安装Go对于完成本书其余部分的练习至关重要。 我们将在本书的后半部分使用Hugo模块。
{{< /hint >}}

下一步是初始化Hugo模块。 每个Hugo模块都需要一个模块名称。 此名称标识模块。 模块名称仅在Hugo模块的上下文中使用。 要初始化名为acmeporationwebsite的模块，请在命令行上运行以下清单中的命令。

{{< details title="Listing 8.1  Hugo command to create a new module" open=true >}}
```
hugo mod init AcmeCorporationWebsite
```
{{< /details >}}

该命令在根文件夹中创建一个名为go.mod的文件。 每个模块都有一个go.mo d文件。 该文件是Hugo模块的入口点。 它标识当前模块，并存储有关该模块链接到的其它模块的信息。 该文件在概念上类似于Ruby中的Gemfile、Node.js中的Package.json和Python的pip中的Requirements s.txt。 它列出了我们在安装和更新过程中可以使用的依赖项及其版本。 我们可以使用此文件扫描直接依赖项列表。 我们应该将此文件检查到版本控制中，并且在Hugo世界中的大多数情况下，我们不会手动修改它。

{{< hint info >}}
**Exercise 8.1**

是非题：如果我们开发的是单一网站，Hugo模块没有任何优势。
{{< /hint >}}

{{< hint info >}}
**为什么有config.yaml还有go.mod**

Hugo模块在很多方面都是Hugo的独特之处。 Go需要安装，它有一个额外的初始化命令，以及一个单独的go.mo d文件。 这种分离是必要的，因为Hugo模块是GO模块上的轻量级包装器。 如果你称之为go mod init，而不是hugo mod init，你会发现它的行为是一样的。 Hugo选择GO模块作为其模块系统的基础，原因有很多：
- 这是一个高性能，维护良好，高度灵活的功能，具有合理的默认值。 你可以链接到从服务器存储库中的单个文件到另一个模块中的文件夹的任何内容。
- Hugo是用围棋建造的。 这不会给使用Hugo的网站增加新的可维护性风险(请记住，在第2.5.2节，每个依赖项都需要额外的维护)。
- 编写和维护涉及管理从internet下载的依赖项的模块系统非常困难。 除了性能，安全性是一个很大的问题。 通过包装Go模块，Hugo团队以低成本获得了强大的功能。
- 标准的go.mod文件有其优点。 审计人员检查Hugo网站需要一个文件，与Hugo web开发框架相比，漏洞检测系统更可能支持Go语言。

Hugo的团队已经构建了一些巧妙的优化并紧密集成到Hugo模块中。 即使你是熟悉Go模块的Go开发人员，Hugo模块也提供了许多惊喜。 Hugo通过自动为go.mod填充文件夹位置的自定义映射以及选择插件类型的能力，实现了Go模块的个性化。 对于Hugo开发人员来说，go.mo d在大多数情况下都是机器生成的文件。 与Resources文件夹一样，go.mod不需要手动操作；只需将其与源代码一起签入。 Hugo可以使用配置找出依赖关系，并自动创建go.mo d文件。
{{< /hint >}}