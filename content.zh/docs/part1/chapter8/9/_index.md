---
weight: 9
title: "8.9 模块作为模板插件"
date: 2022-09-12T18:26:30+08:00
draft: true
---

# 8.9 作为模板插件的模块

我们可以跨多个主题以partials的形式分享Hugo的模板代码。 这些共享的部分可以充当包装可重用函数的插件。 在开发Hugo模板时，一个有用的模块是Hugo debug实用程序，它提供了我们与折衷主题一起使用的调试按钮。 我们将把这个模块添加到AcmeTheme模块，使所有使用这个主题的网站都可以使用。

要使用此模块，我们将其导入config.yaml for AcmeTheme (https:// github.com/hugoinaction/hugoinaction/tree/ chapter-08-resources/03)。   Hugo支持单个模块和配置中的MODULE：Imports部分中的一个列表。 因为我们已经有一个模块，所以我们将需要将module: imports转换为一个列表，以获取多个模块，如下面的列表所示。

{{< details title="Listing 8.8 Importing the debug utilities (AcmeTheme/config.yaml)" open=true >}}
```yaml
module:
    ...
    imports:
        ...
        - path: github.com/hugoinaction/hugo-debug-utils
```
{{< /details >}}

请注意，Hugo调试实用程序已经被初始化为Hugo模块，并在内部提供挂载。 因此，我们不需要手动设置此模块的安装座。 在包含之后，我们可以开始在代码中使用该模块。 Hugo debug实用程序的副本也可在章节资源 (https://github.com/hugo无为/tree/chapter-08-resources/04) 中找到。  在基本模板布局/_Default/Basof.html中，我们可以添加以下清单中的代码，以便在定义脚注块之后加载调试栏。

{{< details title="Listing 8.9  Adding the debug bar (AcmeTheme/layouts/_default/baseof.html)" open=true >}}
![Listing8.9](Listing8.9.svg)
{{< /details >}}    

{{< hint info >}}
**CODE CHECKPOINT**    https://chapter-08-07.hugoinaction.com, and source code: https://github.com/hugoinaction/hugoinaction/tree/chapter-08-07.
{{< /hint >}}

如果我们通过在命令行上发出hugo server来运行实时服务器模式，则该模块将自动下载，并添加到go.mo d和go.sum文件中，并且应该显示调试按钮。 Hugo模块使隔离Hugo依赖项变得简单。 为了了解它是如何工作的，我们可以使用以下代码查看hugo-debug-utils模块中存在的config.yaml文件:
```yaml
module: 
  mounts:
    -source: debug-bar/template
      target: layouts/partials/debug
    -source: debug-bar/css
      target: assets/css
    -source: debug-bar/js
      target: assets/js
    -source: console
      target: layouts/partials/console
```

此模块的挂载在其配置中指定，包括JavaScript、CSS和PARTIAL。 在网站编译期间，Hugo将相应的文件放置在正确的虚拟位置。

Hugo调试实用程序还附带了一个控制台部分，我们可以使用它在浏览器的JavaScript控制台中记录任何Hugo变量。 这在开发模板时极为有用。 假设我们想知道一个表达式的价值。 我们可以将其部分传递给控制台，表达式的值将在浏览器控制台中可用。 下面的清单允许我们查看传递给页面的前置事件参数(使用AcmeTheme/Layout/_Default/Basof.html进行这些更改)。

{{< hint warning >}}
**NOTE** 调试时，你应该只添加以下清单中的代码。
{{< /hint >}}

{{< details title="Listing 8.10  Passing debugging parameters the browser console" open=true >}}
```
{{ partial "console" .Params }}
```
{{< /details >}}