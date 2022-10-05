---
weight: 8
title: "8.8 添加嵌套依赖项"
date: 2022-09-12T18:26:30+08:00
draft: true
---

# 8.8 添加嵌套依赖项

到目前为止，通过Hugo模块，我们已经能够动态加载主题，并为正确使用主题提供一定程度的检查 (如所需的最低Hugo版本)。 雨果模块的主要功能是让主题拥有自己的依赖项，我们现在将使用这一点。 由于将主题转换为Hugo模块，因此可以实现特定于主题的依赖项，因此在安装主题时，这些依赖项将被拉入网站。 在Hugo中，我们可以有各种模块依赖关系，从模板和内容到JavaScript和CSS。

我们可以将依赖项从依赖项中的任何文件夹安装到我们网站中的任何位置。 雨果模块与雨果管道相结合，可以作为一个轻量级捆绑器，为我们的网站链接和引入资源(例如，主题、布局、资产、内容)，作为Java脚本中的NPM+webpack生态系统或Ruby/Rail中的RubyGems链轮的替代方案。 与强制内容挂载到特定文件夹的资产系统 (例如，JavaScript中的node_modules) 不同，Hugo模块可以映射到其文件系统中的任何位置。 我们可以将资源模板文件(*.css.tpl)导入到Assets文件夹中以在网站上使用它们。

e github.com/hugoinaction/AcmeSupport存储库中存在其他支持文件，因此我们将通过Hugo模块导入这些文件。 对于脱机使用，第8章的章节资源还包含此存储库的内容，我们可以使用前面描述的替换指令(https://github.com/hugoinaction/hugoinaction/树/第08章-资源/02)导入这些内容。

首先，我们需要向AcmeSupport存储库添加一个依赖项。 默认情况下，Hugo将所有依赖项导入到Themes文件夹。 由于主题是最常见的依赖项，因此此默认设置允许我们通过指定GitHub位置来导入主题，如第8.3节所述。

默认情况下，Hugo挂载/Themes文件夹中的所有模块。 AcmeSupport存储库由CSS模板文件组成。 因此，我们需要手动覆盖挂载此依赖项的默认位置。 Hugo允许我们在源以及目标存储库中指定挂载点。

AcmeSupport存储库不是Hugo模块； 里面没有go.mo d文件。 尽管如此，我们仍然可以成功地进口它。 要指定其挂载点，我们可以进入集成存储库的配置 (AcmeTheme代码库)，并在模块部分中指定挂载点，如下面的清单所示。 我们将Assets文件夹(源名称可以是任何内容)挂载到主题存储库中的Assets文件夹(目标名称，需要是Assets)。

{{< details title="Listing 8.7 Mounting the AcmeSupport repository (AcmeTheme/config.yaml)" open=true >}}
```yaml
module:
...
  imports:
    path: github.com/hugoinaction/AcmeSupport
    mounts:
      - source: assets
        target: assets
```
{{< /details >}}

{{< hint info >}}
**CODE CHECKPOINT**    https://chapter-08-06.hugoinaction.com, and source code: https://github.com/hugoinaction/hugoinaction/tree/chapter-08-06.
{{< /hint >}}

如果你还记得第6章，我们使用Hugo Pipes将 *.css.tpl文件合并到网站中使用的CSS文件中。 新添加的css.tpl文件会自动包含在我们之前所做的更改中，并在网站上使用。 这个CSS文件 (添加在AcmeSupport存储库中) 颠倒了主页上图像和文本的顺序，如图8.4所示。 图像位于右侧，内容位于左侧。 我们可以用这个来验证模块是否按预期加载。

![Figure8.3](Figure8.3.svg)

图8.3主页上的图片和内容与AcmeSupport互换

如果我们在根目录 (Acme Corporation存储库) 上运行hugo mod vendor，则Hugo会在 _vendo r/github.com/hugoinaction文件夹中创建AcmeSupport文件夹，该文件夹现在包含Git存储库的内容。 Hugo还使用此依赖项更新Acme Corporation网站的go.sum文件。 go.sum文件跟踪项目中使用的依赖项以及子依赖项。 如果我们想要审计网站的依赖关系，go.sum文件是正确的选择。

{{< hint info >}}
**Exercise 8.2**

go.mo d文件中存在哪些信息？(选择所有适用的。)
- a. Name of the module
- b. Version of Hugo used to create the module
- c. List of dependencies (both direct and indirect) of the website
- d. Exact hashes of each website dependency
- e. Mount paths for various folders in the repository
{{< /hint >}}

我们可以根据需要装载任意多的子文件夹，因为配置文件中的mount选项包含源和目标装载位置的列表。 此选项允许我们导入我们的JavaScript和CSS依赖项，而不需要将原始存储库设置为Hugo模块，甚至将Hugo理解为一个概念，这将整个internet作为Hugo网站的内容来源。受欢迎

JavaScript/CSS libraries like Bootstrap (https://getbootstrap.com), jQuery (https:// jquery.com), etc., can be linked via this method. We could also link icon packs like FontAwesome  (https://fontawesome.com)  or  SCSS  toolkits  like  Bourbon  (https:// www.bourbon.io).

{{< hint warning >}}
**NOTE** 即使你计划将主题用于单个网站，使用Hugo模块也可以链接到主题之外的依赖项。 通过模块链接而不是复制提供了快速更新依赖并更好地跟踪代码段所有权的好处。 我们还可以有子依赖关系，这使得这一点非常灵活。
{{< /hint >}}