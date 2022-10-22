---
weight: 5
title: "8.5 获取主题的特定版本"
date: 2022-09-12T18:26:30+08:00
draft: true
---

# 8.5 获取主题的特定版本

Hugo Modules通过Git标签支持版本。 这允许我们链接到不同版本的依赖项，而不是最新的主线。 在许多项目中，mainline处于积极开发状态，并且在单独标记发布版本时不稳定。 我们将切换回带有Hugo模块的AcmeTheme。 AcmeTheme的副本位于e github.com/hugoinaction/AcmeTheme文件夹的GitHub上，在本书的第8.5节 (本节) 中，其内容标记为0.8.0版。

{{< hint warning >}}
**NOTE** 不要在GitHub上使用Acme存储库的主分支，因为它指向本书末尾的AcmeTheme模块。
{{< /hint >}}

要获得主题的特定版本，我们需要像以前一样指定主题，但是我们不会告诉Hugo通过Hugo服务器自动获取最新版本，而是手动告诉Hugo要获取的版本。 让我们首先在配置中将主题更改为托管的AcmeTheme存储库，如下面的清单所示。

{{< details title="Listing 8.3 Switching to the AcmeTheme repository (config/_default/config.yaml)" open=true >}}
```yaml
theme: github.com/hugoinaction/AcmeTheme
```
{{< /details >}}

{{< hint warning >}}
**NOTE** 更新到AcmeTheme时，live server不应该运行，此时我们不应该调用hugo server。 这将导致AcmeTheme主分支的安装。
{{< /hint >}}

接下来，我们需要从v0.8.0标签安装主题。 有两种方法可以做到这一点：手动向go.mod文件添加条目或从命令行运行安装命令。 hugo mod子命令与Hugo模块相关联，这些模块提供对与Hugo模块相关的管理功能的访问。 我们使用Hugo mod init来定义一个组成我们网站的新模块。 hugo mod get命令手动获取基于模块的依赖项。 U命令行标志会覆盖go.mod中的现有条目(如果存在)。 以下列表为v0.8.0版本的go.mo d文件添加了一个条目。

{{< details title="Listing 8.4  Adding a specific version of AcmeTheme" open=true >}}
```shell
hugo mod get -u github.com/hugoinaction/AcmeTheme@v0.8.0
```
{{< /details >}}

使用此命令，你应该在go.mod文件中看到Required githorb.com/hugoinaction/AcmeTheme v0.8.0//Inditive。 校验和文件go.sum还应包含 “v0.8.0” 作为AcmeTheme依赖关系的安装版本。

我们可以继续使用我们的网站与AcmeTheme链接作为一个模块在Hugo。 我们已经完全摆脱了这一变化的折衷主义，并接管了Acme Corporation网站的完全控制权，我们拥有每一段代码。 在本书的其余部分，我们不会使用折衷或通用。 我们可以删除配置中特定于这些主题的条目 (除了config/_default/params.yaml中的颜色和版权)，也可以删除资产/图像/background.svg、资产/图像/徽标.svg、内容/data-driven.md，静态/image/* 和静态/favicon.ico文件，我们在主题Acme中不使用这些文件。 如果愿意，我们可以删除Themes/AcmeTheme文件夹，网站仍将继续运行。

{{< hint info >}}
**CODE CHECKPOINT**    https://chapter-08-03.hugoinaction.com, and source code: https://github.com/hugoinaction/hugoinaction/tree/chapter-08-03.
{{< /hint >}}