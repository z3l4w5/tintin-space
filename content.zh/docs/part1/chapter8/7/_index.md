---
weight: 8
title: "8.7 在本地修改依赖关系"
date: 2022-09-12T18:26:30+08:00
draft: true
---

# 8.7 在本地修改依赖项

我们可以更改 _vendor文件夹的内容，并在Hugo中实时查看更改，但这是一个不好的做法。 下次更新依赖项时，我们所做的更改将被覆盖。 将每个提交推送到主题存储库也可能令人厌烦。 Hugo有一种机制可以为本地开发提供托管依赖项的本地版本。 我们需要将依赖项 (在这种情况下为AcmeTheme) 设置为Hugo模块来启用此功能。 要执行此任务，请转到主题文件夹并运行以下命令：

```shell
hugo mod init AcmeTheme (Initializes the module with the name AcmeTheme)
```

此命令在主题的文件夹中创建一个go.mod文件。 通过此更改，模块系统可以将AcmeTheme读取为不只是一个文件夹，而是一个适当的Hugo模块。 接下来，我们可以在go.mo d中使用要求调用下的replace指令为Acme Corporation网站提供此模块的路径，如下面的列表所示。

{{< details title="Listing 8.5 Adding the path to AcmeTheme for local development (go.mod)" open=true >}}
```
module AcmeCorporationWebsite

...

replace github.com/hugoinaction/AcmeTheme =>
    <Absolute or relative path to the theme>.
```
{{< /details >}}

有了这个REPLACE指令，我们可以很容易地在一个独立的存储库中继续本地开发，并仍然使用Hugo模块引用它。 在本书呈现的代码示例中，我们将使用代码存储库中的AcmeTheme文件夹来托管主题。 只有主题的最终版本(在本书的末尾)才会被推送到githorb.com/hugoinaction/acme文件夹。 因为存在 _vendor文件夹，所以在我们删除优先级更高的 _vendor文件夹之前，replace指令不会生效。 我们应该使用_Vendor文件夹进行存档，而不是进行开发。 虽然在主题没有改变 (只有内容改变) 的情况下使用这个是很好的，但是当我们开发主题时，这是一个障碍，所以我们会删除它。

我们已经创建了一个新模块，我们计划在Acme Corporation网站之外使用。 申报它的要求是一个好主意，这样其它地方就可以进口它了。 Hugo的包管理需要两个文件: go.mo d和config。 Go.mod文件列出依赖项，而配置文件提供配置和包信息。

因为AcmeTheme还没有一个庞大的配置，所以配置文件夹就太过分了。 我们将在主题的文件夹 (https:// github.com/hugoinaction/hugoinaction/tree/ chapter-08-resources/01) 中放置一个简单的config.yaml。 在配置中，我们可以指定该特定模块所依赖的Hugo的最低和最高版本，以及是否需要Hugo扩展。 尽管不是必需的，但最好指定主题所需的最低版本的Hugo。 我们在下面的清单中执行此操作。

{{< details title="Listing 8.6 Specifying the minimum version of Hugo (AcmeTheme/config.yaml)" open=true >}}
```yaml
module: 
  hugoVersion:
    min: 0.91.2
```
{{< /details >}}

{{< hint info >}}
**CODE CHECKPOINT**    https://chapter-08-05.hugoinaction.com, and source code: https://github.com/hugoinaction/hugoinaction/tree/chapter-08-05.
{{< /hint >}}