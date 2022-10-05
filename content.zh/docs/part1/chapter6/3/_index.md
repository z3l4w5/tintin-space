---
weight: 3
title: "6.3 Hugo Pipes的资产处理"
date: 2022-09-12T18:26:30+08:00
draft: true
---

# 6.3 用雨果管道处理资产

通过将HTML生成移至Hugo的模板系统，我们大大简化了HTML生成的工作，我们现在可以基于标记文档来完成。 然而，图像和其他资源(如JavaScript和CSS)仍然存在问题。 在更改宽高比和将图像调整大小为缩略图、移动设备、桌面等多个文件方面，我们需要做很多工作来获得良好的性能。 此外，要成为基于标记或元数据的，需要有一种方法使基于标记的信息进入到JavaScript或CSS中。 雨果管是雨果对这些问题的解答。

Hugo提供了实用程序方法来管理来自页面包、全局资产文件夹和所提供的任何文件路径的资源。 这些方法中的大多数都采用单个参数，我们将它们与第5.1.7节中讨论的管道操作员一起使用。 雨果管道是雨果用于资源管理的一组功能。

## 6.3.1 处理文本资产

我们目前正在使用静态文件夹来存储Backack.svg、index.css和logo.svg资产，而不是Favic.ico。 (logo.png用于通用主题，当我们删除对该主题的支持时，我们将删除该主题。) 我们可以将所有这些文件移动到Assets文件夹，并使用Hugo Pipes进一步处理它们。 Hugo支持将管道用于所有基于文本的文件格式。

让我们从index.css开始。 下面的清单使用Hugo Pipes读取CSS文件。 然后，我们需要将index.css文件移动到Assets文件夹，这样才能正常工作。   最后，我们可以使用resources API加载此文件。

{{< details title="Listing 6.24  Reading the CSS file (layouts/modern/baseof.html)" open=true >}}
{{ $css := resources.GetMatch "index.css"}}
<link rel="stylesheet" type="text/css" href="{{$css.Permalink}}">
{{< /details >}}

{{< hint info >}}
**CODE CHECKPOINT**	https://chapter-06-13.hugoinaction.com, and source code: https://github.com/hugoinaction/hugoinaction/tree/chapter-06-13.
{{< /hint >}}

有了resource ces.GetMatch，我们可以将默认文件放在网站中要覆盖的主题的资产文件夹中。 请注意，我们之前在products.csv文件中使用了相同的功能。 要获得准确的资源，我们可以使用resource.Get，尽管GetMatch支持通配符(也称为GLOB)。

Hugo Pipes的真正力量伴随着对加工的支持。 Hugo可以使用SCSS处理器(仅在扩展风格中)和PostCSS后处理器处理CSS文件。 SCSS (或SASS) 是一种CSS超集语言，支持CSS中的嵌套，功能和编译时变量。SCSS背后的理念是编译时优化和代码生成。这种方法与Jamstack的方法相匹配，并且两者可以很好地协同工作。让我们将assets/index.css文件重命名为assets/index.scss，并通过Hugo Pipes使用SCSS预处理器使用 $ css := resources.GetMatch “index.css” | resources.ToCSS

First, we need to verify if the version of Hugo we have installed is the extended ver- sion. For that, let’s run the command hugo version on the command line. If you have the extended version of Hugo installed, you should see extended in the command- line output:

Hugo Static Site Generator v0.91.2/扩展

SASS编译器有两种风格: 嵌入在Hugo中的不需要单独二进制文件的版本(LibSass)，以及sass编译器作为外部进程运行的版本(Dart Sass)。 Dart Sass更新且功能丰富，但是我们需要一个外部脚本来安装它。 我们可以配置要在网站配置中使用的SASS编译器。

你将需要Hugo的扩展版本才能使用SCSS功能。 请注意，在许多平台(包括Windows上的巧克力)中，默认情况下，包管理器会安装Hugo的常规(非扩展)版本。 使用扩展版本没有坏处，因为更大的编译器二进制文件对最终输出大小或性能没有影响。 清单6.25为我们将SCSS编译成了CSS。

{{< hint warning >}}
**NOTE** 你不需要SCSS来完成本书中的代码示例。 如果你没有安装Hugo Extended，你可以跳过这个特定的代码检查点，继续阅读本书的其余部分。
{{< /hint >}}

{{< details title="Listing 6.25   Compiling SCSS into CSS (layouts/modern/baseof.html)" open=true >}}
{{ $css := resources.GetMatch "index.scss" | resources.ToCSS }}
{{< /details >}}

{{< hint info >}}
**CODE CHECKPOINT**	https://chapter-06-14.hugoinaction.com, and source code: https://github.com/hugoinaction/hugoinaction/tree/chapter-06-14.
{{< /hint >}}

雨果不在乎文件名扩展名。 如果需要，我们可以通过SCSS代码转换器传递index.css。 SCSS超出了本书的范围。 这对雨果来说不是必要的，我们也不会深入探讨。 我们只需要用于样式内容的CSS，这是SCSS编译的输出。 对于不想使用扩展版的Hugo的读者，我们将恢复这一更改，尽管你可以自由地继续使用你的网站的SCSS。

我们可以通过资源将PostCSS处理器用于CSS。Postcss(需要安装postcss-cli)，无需任何配置更改。 我们还可以通过Babel转编程序处理JavaScript文件 (需要安装 @ babel/cli和 @ babel/core)，以便通过旧版本的web浏览器的babel管道访问未来的JavaScript功能。 一种更好的方法是使用Hugo的内置JavaScript绑定器js.Build (我们将在第10章中讨论js.Build)。

{{< hint info >}}
**NOTE** Hugo与JavaScript生态系统进行了特殊的集成。 第10章完全致力于在基于Hugo的网站中使用JavaScript。
{{< /hint >}}

当使用带有Hugo管道的CSS/JS处理器时，我们可以通过Hugo模板解析器运行JavaScript或CSS文件，完全访问变量、函数和部分参数的整个系统，并使其内容像HTML一样由数据驱动。 Acme Corporation网站的主题颜色目前为蓝色。 如果我们将其移至模板系统，则可以从Acme配置文件进行控制。 我们已经在config.yaml中将此颜色定义为参数中的颜色。 我们可以通过{{site.Param“COLOR”}}访问该参数。 请记住，从第5章开始，站点是Hugo为站点变量提供的全局变量。 它在所有部分以及模板中都可用。 使用site而不是 $.Site在跨部分使用此模板时提供了最大的灵活性。

虽然颜色值存在于配置中，但我们不会在index.css和ackek.svg中使用它，这两个文件当前使用硬编码值“#4f46e5”。 我们需要这些值是动态的，这样我们就可以在配置中的一个地方改变它们。 为此，我们需要将这些文件转换为模板。 然后，我们可以通过此运行Hugo的模板渲染，并在编译时生成网站的实际文件。 Hugo提供了一个名为resource ces.ExecuteAsTemplate的函数，可以将任何资源文件作为Hugo模板进行处理。 为此，我们将从logo.svg和background.svg开始。

让我们创建这些文件的副本，并为其添加.tpl扩展名。 虽然不是必需的，但重命名模板文件并添加是一个好主意。tpl扩展以帮助识别。  接下来，我们需要将这些文件(https://github.com/hugoinaction/hugoinaction/tree/chapter-06-resources/04).中出现的所有“#4f46e5”替换为{{site.Params.color|Default“#4f46e5”}} 请注意，我们不会删除旧的background.svg和logo.svg，直到第8章，我们完全摆脱折衷的主题。 清单6.26提供了更改到Backack.svg模板的代码，这样我们就可以使用提供的主题颜色了。 然后列出6.27更改logo.svg模板。

{{< details title="Listing 6.26   Changing background.svg (assets/image/background.svg.tpl)" open=true >}}
```html
<style type="text/css">
...
.st2{fill:none;stroke:{{site.Params.color | default "#4f46e5"}};
stroke-width:4;stroke-miterlimit:10;opacity: 0.2}
...
.st6{fill:{{site.Params.color | default "#4f46e5"}}; opacity: 0.2}
...
</style>
```
{{< /details >}}

{{< details title="Listing 6.27    Changing logo.svg (assets/image/logo.svg.tpl)" open=true >}}
```
<style type="text/css">
.st0{fill:{{site.Params.color | default "#4f46e5"}};}
...
</style>
```
{{< /details >}}

Acme Corporation网站的css文件使用每个颜色分量(红、绿和蓝)的css自定义属性来定义其主题。 如果我们简单地用颜色值编码，用 {{site.Params.color}} 替换 “#4f46e5” 就足够了。 对于传递单个颜色值，我们需要做更多的工作。 以下列表为Hugo的CSS变量提供了单独的主题颜色。

{{< details title="Listing 6.28  Providing individual theme colors (assets/index.css.tpl)" open=true >}}
![Listing6.28](Listing6.28.svg)
{{< /details >}}    

该CSS文件还包含具有硬编码背景颜色RGB(79、70、229)的背景SVG图像。 我们应该在整个文件中做一个查找和替换操作，将硬编码的颜色值替换为rgb({{$r}},{{$g}},{{$b}})。 我们不能在这里直接使用$COLOR，因为它需要URL编码。

接下来，我们需要通过资源将这些文件加载到我们的网站中。ExecuteAsTemplate，如以下清单所示。 我们还将通过resources.minify传输输出以减小其文件大小。

{{< details title="Listing 6.29 Parsing index.css.tpl (layouts/modern/baseof.html)" open=true >}}
```
{{ $css := resources.GetMatch "index.css.tpl"
| resources.ExecuteAsTemplate "index.css" "nothing"
| resources.Minify }}
```
{{< /details >}}
    	
资源.ExecuteAsTemplate接受目标文件的名称和可传递给模板的上下文变量。 像partials一样，资源模板在孤立的环境中执行，$ 变量由我们直接传递的数据组成。 其原因与部分原因相同： 以允许最大限度地重用缓存。 因为SITE变量是全局可用的，所以我们不需要模板执行的参数。 完成此操作后，我们可以通过解析并执行与index.css类似的方式来加载基本模板中的徽标.svg。 下面的清单显示了此过程。

{{< details title="Listing 6.30  Parsing logo.svg.tpl (layouts/modern/baseof.html)" open=true >}}
```
{{ $logo := resources.GetMatch "image/logo.svg.tpl"
| resources.ExecuteAsTemplate "logo.svg" "nothing"
| resources.Minify }}
<img src="{{$logo.Permalink}}" alt="Acme Logo"
width="48" />
```
{{< /details >}}

我们可以更新index.css.tpl来渲染background.svg模板。 下面的清单显示了如何更新index.css以使用.tpl文件实现这一点。

{{< details title="Listing 6.31  Updating index.css for background.svg (assets/index.css.tpl)" open=true >}}
```html
{{ $background := resources.GetMatch "image/background.svg.tpl" |
resources.ExecuteAsTemplate "background.svg" "nothing" | resources.Minify}} background: url({{$background.Permalink}}) 0 0/cover;
```
{{< /details >}}

{{< hint warning >}}
**NOTE** 如果我们使用resources.Executeastempate，Hugo的缓存机制就会受到损害。 强烈建议在Partial中使用资源.ExecuteAsTemplate，并使用artialCached调用它，以防止不必要的重新计算。 我们将移动logo.svg和index.css解析成单独的部分作为读者的练习。
{{< /hint >}}

{{< hint info >}}
**CODE CHECKPOINT**     https://chapter-06-15.hugoinaction.com, and source code: https://github.com/hugoinaction/hugoinaction/tree/chapter-06-15.
{{< /hint >}}

现在我们可以控制网站配置中的颜色(例如，设置为“#DC2626”)，以获得网站的不同主题颜色(如图6.4所示)，以便在本书的其余部分使用。

{{< hint info >}}
**CODE CHECKPOINT**     https://chapter-06-16.hugoinaction.com, and source code: https://github.com/hugoinaction/hugoinaction/tree/chapter-06-16.
{{< /hint >}}


{{< figure src="Figure6.4.svg" title="图6.4将配置文件中的网站主题颜色更改为 \"#DC2626\"" >}}

另一个重要的特性是支持css连接。 Hugo可以轻松地将多个CSS文件合并为一个以发布，但是我们不能连接图像。 在第6章的参考资料中，你将找到文件addtional.css.tpl  (https://github .com/hugointoption/tree/chapter-06-resources/05)。 我们可以将此文件放在Assets文件夹中以供使用。 然后我们可以使用resources.Concat连接它 请注意resources.Concat需要有效的MIME类型才能工作。 因此，对于concat API，我们将使用index.css而不是index.css.tpl。 下面的清单使用此API允许通过单个调用加载多个CSS模板。

{{< details title="Listing 6.32  Using the concat API (layouts/partials/index.css.html)" open=true >}}
![Listing6.32](Listing6.32.svg)
{{< /details >}}

{{< hint info >}}
**CODE CHECKPOINT**	https://chapter-06-17.hugoinaction.com, and source code: https://github.com/hugoinaction/hugoinaction/tree/chapter-06-17.
{{< /hint >}}

要获得匹配glob模式的所有文件的切片 (数组)，我们可以使用resources.Match。 这样，我们就可以开发独立的文件，并在生产中提供合并的版本。 请注意，additional.css在网站标头上的设计中提供了微妙的更改，我们可以使用它来验证此文件的加载。

{{< hint info >}}
**Exercise 6.4**

将英雄形象添加到Acme Corporation网站主页。 英雄图像在章节资源(https://github.com/hugoinaction/hugoinaction/tree/chapter-06-resources/06).中以svg图像的形式提供 生成的HTML应该与https://chapter-06-18.hugoinaction.com匹配，动态生成的SVG图像，以便与网站颜色匹配。 下图显示了添加图像后的主页。

![Figure6_](Figure6_.svg)
{{< /hint >}}

{{< hint info >}}
**CODE CHECKPOINT**	https://chapter-06-18.hugoinaction.com, and source code: https://github.com/hugoinaction/hugoinaction/tree/chapter-06-18.
{{< /hint >}}

## 6.3.2 处理图像

虽然矢量图形和svg非常适合文件大小，但并非所有内容都可以使用矢量图形轻松构建。 像JPEG和PNG这样的栅格图像是现代网络的重要组成部分，构成了许多网站的大部分网络流量。
Hugo Pipes广泛支持这些图像，包括使我们能够为通过web进行最佳交付做好准备的操作。 虽然我们的博客帖子有图片，但我们不会在网站的索引页面上使用这些图片。没有图片，我们的博客帖子看起来不完整。

要为博客文章添加封面图片，可以通过resources.GetMatch访问全局资产位置中的资源。 下面的清单显示了如何通过Page.Resources.GetMatch访问页面包中的资源以添加封面图片。

{{< details title="Listing 6.33  Adding a cover image for blog posts (layouts/modern/index.html)" open=true >}}
```html
<li class="post">
<a href="{{.Permalink}}">
{{$title := .Title}}
{{with (.Resources.GetMatch "cover.*")}}
<img alt="{{$title}}" loading="lazy" src="{{.Permalink}}" />
{{end}}
...
</a>
</li>
```
{{< /details >}}

{{< hint info >}}
**CODE CHECKPOINT**	https://chapter-06-19.hugoinaction.com, and source code: https://github.com/hugoinaction/hugoinaction/tree/chapter-06-19.
{{< /hint >}}

之前清单中的代码存在明显的性能问题。 博客帖子的封面图片很大，像素超过了在主页的小视图中呈现它们所需的像素。 我们无法在页面包中调整它们的大小，因为单个页面需要更大的图像。 Hugo支持在编译期间为此用途动态调整图像大小。 以下是Hugo中的调整大小选项:

    .Resize—This option resizes the image. It can take parameters in the form of the desired width and height. For example, {{ $hero.Resize "200x200"}} resizes the hero image to 200×200 px, ignoring the aspect ratio. If we use
{{ $hero.Resize "200x"}}, the image is resized to the width of 200 px with the height based on the aspect ratio, and {{ $hero.Resize "x200"}} resizes the image to the height of 200 px with the width calculated based on the original aspect ratio.

    .Fit—此选项会调整图像大小，使其适合所提供的框。 例如，{{ $hero.Fit "200x200"}}确保宽度或高度为200像素，而另一个尺寸(高度或宽度)小于200像素。 1000 × 800图像将缩小到200 × 160，而800 × 1000图像将变为160 × 200。 这类似于CSS属性object-fit: container或back-ground-fit：container。

    .Fill—此选项会调整图像大小，以在裁剪外部零件时填充所提供的框。 For example, {{ $hero.Fill "200x200"}} creates a 200×200 image where the image would be resized and cropped either in the length or      the breadth. This is equivalent to object-fit: cover or background-fit: cover. .Fill in Hugo can also take an optional parameter that defines the part of the image to keep. For example, if we use .Fill "200x200 left", Hugo leaves the leftmost part of the image intact. Hugo also offers an option called smart, where Hugo automatically detects the important part of the image.

{{< hint info >}}
**进一步优化**

虽然Hugo按照提供的参数处理资产，但资产的进一步优化仍然是可能的。 许多开发人员使用对Hugo的输出进行后处理来进一步优化。 包括Netlify在内的大多数主机都将资产优化作为其CDN主机的一项功能。

我们可以包含用于此处理的特定插件。 我们可以通过获取公共或docs文件夹的内容并通过诸如ImageOptim，CSS通过CSSMin和JavaScript之类的工具传递图像来手动进行后处理，以进一步优化生成的资产。 我们还可以使用img标记中的HTML图片标记或srcset属性，为浏览器提供基于视区大小加载正确图像的选项。
{{< /hint >}}

主屏幕上的封面图像所需的最大尺寸的宽度约为1000 px (以处理高密度显示中的2倍缩放)。 下面的清单显示了如何使用.ReSize选项将封面图像限制为较小的大小。 我们还添加了loading=lazy来懒惰地加载这些图像，从而加快了网站的初始渲染速度。 请注意，延迟加载是一种HTML，而不是Hugo的性能特性。

{{< details title="Listing 6.34  Resizing the cover image for blogs (layouts/modern/index.html)" open=true >}}
<img alt="{{.Title}}" loading="lazy"
src="{{((.Resources.GetMatch "cover.*").Resize "1000x").Permalink}}" />
{{< /details >}}   

根据文件大小，此代码在加载索引页时提供了大量节省。 强烈建议将图像转换为WebP格式，这样可以进一步减小文件大小。 我们可以通过webp作为选项。调整大小 (例如.Resize “1000x webp” 的大小)。 如果我们使用Hugo的扩展Flavor，此选项会将图像转换为WebP格式。 WebP有> 95% 浏览器的采用，除非我们针对古代浏览器，否则使用WebP作为我们网站上图像的唯一格式是安全的。 如果需要较旧的浏览器支持，我们可以使用HTMLPicture标签来提供WebP和JPEG/PNG版本的图像。 为了保持对Hugo optional扩展版本的依赖，我们在本书中不使用WebP。

{{< hint info >}}
**CODE CHECKPOINT**	https://chapter-06-20.hugoinaction.com, and source code: https://github.com/hugoinaction/hugoinaction/tree/chapter-06-20.
{{< /hint >}}

我们还可以为图像提供艺术滤镜，如模糊、深褐色或灰度。 图6.5包括这些过滤器中的一些过滤器的列表。

Acme Corporation网站的图标仍然是与硬编码的“旧”主题相同的颜色。 不幸的是，由于各种浏览器供应商对SVG favicons的支持不稳定，我们需要至少将favicon的PNG副本链接到我们的网站。 我们可以使用雨果的图像处理滤镜，使用主题颜色(https://github.com/hugoinaction/hugoinaction/tree/chapter-06-resources/08).对我们最喜欢的图标重新着色

{{< figure src="Figure6.5.svg" title="图6.5 Hugo中的图像处理和过滤器支持。 HUGO支持多种选项来调整大小以及使用滤镜(https://github.com/hugoinaction/hugoinaction/tree/chapter-06-resources/07).处理图像" >}}

请注意，这里的数学是复杂的，虽然它展示了雨果提供的灵活性，但在大多数情况下，你不需要这样复杂的东西。 我们将计算缓存部分中的收藏图标，以防止重新运行我们的计算，然后在我们网站的Head部分使用它。 下面的清单显示了如何使用配置中存在的颜色动态地重新着色favicon。

{{< details title="Listing 6.35 Recoloring the favicon (layouts/partials/favicon.png.html)" open=true >}}
![Listing6.35](Listing6.35.svg)
{{< /details >}}    	

为了理解正在发生的事情，让我们举一个例子。 假设我们要将图标重新着色为rgb(220，38,38)。 我们首先将定义此颜色的所有内容转换为白色、RGB(255,255,255)，而将图像的其余部分转换为透明。 接下来我们计算RGB值:

```
r1 = (220/255 - 1) * 100 = -13.73%
g1 = (38/255 - 1) * 100 = -85.10%
b1 = (38/255 - 1) * 100 = -85.10%
```

使用这些作为颜色平衡滤镜，我们现在可以使用新的RGB值对图像重新着色：

```
Color balance = current color + current color * balance shift

newR = 255 - 255 x 13.73/100 = 220
newG = 255 - 255 x 85.10/100 = 38
newB = 255 - 255 x 85.10/100 = 38
```

我们可以在基本模板的头部部分调用它来加载favicon。 下面的清单显示了这方面的代码。

{{< details title="Listing 6.36  Loading the favicon (layouts/modern/baseof.html)" open=true >}}
```html
<link rel="icon"
type="image/png" href="{{partialCached "favicon.png.html" $ "nothing"}}">
```
{{< /details >}}    	

{{< hint info >}}
**CODE CHECKPOINT**	https://chapter-06-21.hugoinaction.com, and source code: https://github.com/hugoinaction/hugoinaction/tree/chapter-06-21.
{{< /hint >}}

我们可以重做 “索引” 页面上的 “产品” 部分，以包括带有产品图像的卡片列表，而不是使用表格，并为这些卡片提供评级。 我们已经有了除产品图片以外的所有信息，产品图片在第章资源(https://github.com/hugoinaction/hugoinaction/tree/chapter-06-资源/09中提供)。 由于Acme Corporation出售图像，因此我们不想通过internet公开原始图像。 Hugo提供了对覆盖滤镜的支持，我们可以使用它来提供水印。 以下列表添加水印，然后使用Unicode stars (& star; 和 & starf;) 提供星级。 图6.6显示了一张完整的卡片。

{{< details title="Listing 6.37 Showing products as cards (layouts/modern/index.html)" open=true >}}
![Listing6.37](Listing6.37.svg)
{{< /details >}}    

我们不需要将其移至部分。 如果没有任何变化，雨果不会重新计算图像。 缓存的部分有帮助的情况是当存在动态计算时，例如在favicon中执行svg和颜色计算。

{{< hint info >}}
**TIP** 与SVG和字体图标相比，Unicode符号大大节省了字节数。
{{< /hint >}}

{{< figure src="Figure6.6.svg" title="图6.6为产品添加卡片。Hugo提供了将图像叠加到另一个图像上以创建水印的支持。" >}}

{{< hint info >}}
**CODE CHECKPOINT**	https://chapter-06-22.hugoinaction.com, and source code: https://github.com/hugoinaction/hugoinaction/tree/chapter-06-22.
{{< /hint >}}

## 6.3.3 其他资产

我们还可以使用Hugo Pipes访问其他非文本资产，例如pdf，ZIPs或其他二进制内容文件。 尽管Hugo不理解它们的内容，但我们可以使用指向这些文件的准确的相对和绝对链接。 如果文件丢失，则构建失败。 如果我们删除使用该文件的代码，该文件不会复制到输出目录。 这些功能使得使用Hugo管道有一个空的静态文件夹并复制内容是值得的。

{{< hint info >}}
**Exercise 6.5**

以下哪些是使用Hugo管道而不是在Hugo外部预建内容或使用浏览器JavaScript的原因？ (选择所有适用的。)
- a. 当用户请求数据时，Hugo管道运行，因此，对于从未请求的数据，不会发生不必要的执行。
- b. Hugo Pipes可以访问网站配置和前端内容，我们可以在其中合并所有网站设置，例如主题颜色，这些设置可以通过Hugo传递给相关的JavaScript，CSS或图像代码。
- c. Hugo Pipes可以跨版本缓存文件，只有在内容发生变化时才会更新。
- d. Hugo Pipes可以根据需要为图像生成多个尺寸，并且尺寸要求可以通过代码中的简单字符串替换来更改。
{{< /hint >}}