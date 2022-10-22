---
weight: 12
title: "8.12 常用的Hugo模块API"
date: 2022-09-12T18:26:30+08:00
draft: true
---

# 8.12 常用Hugo模块接口

运行hugo mod提供了各种各样的子命令，这些子命令在管理我们日常生活中的模块中很有用。 例如,
- hugo mod tidy—从go.sum和go.mo d文件中删除未使用的条目 (如摆脱折衷)。
- hug mod clean—清除模块缓存以获取较新的更改(如果在本地完成)。有时，本地存储可能会损坏，为我们提供不正确的数据。
- hugo mod graph—显示当前网站或模块的依赖项列表。 理解go.sum可能具有挑战性，但是hugo mod graph使该文件具有人类可读性。
- hugo mod get -u—Updates all modules.
- {hugo mod get -u ./...}—Updates all modules and their dependencies.
- hugo mod get <module>@<version>—Gets a specific version of a module.

记住，当我们开始使用Hugo模块时，我们添加了折中主题作为一个模块来尝试它。 它仍然存在于go.Mo d and go.sum中。 它让我们在不使用的时候下载，造成了不必要的带宽浪费。 我们可以使用hugo mod tidy从go.mo d和go.sum文件中消除未使用的条目。

{{< hint info >}}
**CODE CHECKPOINT**    https://chapter-08-10.hugoinaction.com, and source code: https://github.com/hugoinaction/hugoinaction/tree/chapter-08-10.
{{< /hint >}}

清除依赖项后，可以使用Hugo mod图查看正确的依赖项列表，如清单8.14所示。 此命令提供了Hugo网站中积极使用的依赖项列表。

{{< hint info >}}
**Exercise 8.4**

是非题: 每次我们建立基于Hugo的网站时，都会自动下载Hugo模块。
{{< /hint >}}

{{< details title="Listing 8.14 Getting the Acme Corporation website’s dependency list" open=true >}}
```shell
> hugo mod graph
AcmeCorporationWebsite github.com/hugoinaction/
➥ TermsAndPrivacy@v0.0.0-20200223231951-1c7c1972007a AcmeCorporationWebsite github.com/hugoinaction/
➥ AcmeCommon@v0.0.0-20210710221623-ca55f92c01bc AcmeCorporationWebsite github.com/hugoinaction/
➥ AcmeTheme@v0.8.0 => <path>/AcmeTheme github.com/hugoinaction/AcmeTheme@v0.8.0 github.com/hugoinaction/
➥ AcmeSupport@v0.0.0-20210710141629-d5aef37e0e9c
github.com/hugoinaction/AcmeTheme@v0.8.0 github.com/hugoinaction/
➥ hugo-debug-utils@v0.0.0-20200427035302-d4636e5c27cf
```
{{< /details >}}

{{< hint info >}}
**TIP** 在运行开发服务器时，如果你遇到与网站代码无关的错误，则Hugo的模块缓存可能已损坏。 Hugo将其缓存保留在临时数据文件夹中，以便操作系统在需要时可以回收空间。 因为这些数据是可公开访问的，所以它可能会被破坏，从而导致奇怪的错误。 面对此类问题时，最好的解决方案是使用hugo mod clean完全清除缓存。 Hugo在下一次发射时重新获取数据。
{{< /hint >}}

本章完成了《Hugo在行动》的第一部分。 在本书的第二部分中，我们将跳出完全静态网站的界限，看看Hugo如何与Jamstack的其余部分交互。 我们将继续通过联系页面，基于JSON的API，小型搜索引擎来完成Acme Corporation网站，然后使用Hugo在我们的网站中创建一个电子商务区域。 随着我们继续引入和学习更多的Hugo功能来简化Web开发，我们将发现Hugo模板语言及其功能中的一些隐藏的宝石，这些功能比表面上显示的要多得多。