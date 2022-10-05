---
weight: 1
title: "5.1 将数据和设计分开"
date: 2022-09-12T18:26:30+08:00
draft: true
---

# 5.1 分离数据和设计

要使用标记文档控制网站的索引页，我们需要首先创建标记文档。 content文件夹是整个网站的branch bundle。 我们需要将_index.md(https://github.com/hugoinaction/hugoinaction/tree/chapter-05-resources/01)放在该文件夹中以表示/index.html网页。 请注意，如果我们使用index.md代替，则网站的根将成为leaf bundle，并且不会使用我们在layouts文件夹中提供的模板。 有了标记文档，我们就可以将当前硬编码在index.html中的数据移到这个标记文档的前面。 下面的清单显示了使用Markdown作为标记语言的索引页的内容。 我们将在index.html页面中使用此信息。

{{< details title="Listing 5.1  The contents of the index page in Markdown (content/_index.md)" open=true >}}
```yaml
---
title: Acme Corporation 
description: Welcome to the website of Acme Corporation, the 
 leading creator of digital shapes on the planet, providing 
 precise shape creations that are ready to use. 
subtitle: shaping the world for you to live in 
explore: blog 
---
```
{{< /details >}}    

## 5.1.1 访问Go模板语言

Hugo使用与Go编程语言不同的Go模板语言来创建模板。 Go模板语言可通过模板页面中的超文本标记语言进行访问，方法是使用双花括号({{…}})，也称为花括号标签。

附录D提供了Go模板语言的简短概述。 本章的资源还包括一个名为template-playground的文件夹，我们可以将它放在layout文件夹中，并使用Hugo的模板技术。 如果我们将template.md放在内容文件夹中 (https://github.com/hugoinaction/hugoinaction/tree/chapter-05-resources/02)，则可以从/template端点查看相应的更改。 虽然这本书介绍了Hugo的大多数常用功能，但如果你正在寻找其功能的更全面的列表(附录之外)， Hugo在https://gohugo.io/documentation/上的官方文档列出了这些内容。

Hugo将胡须标记之外的内容视为一个原始字符串，我们可以将其原样传递给最终的HTML。 内容文件夹中存在的所有信息也可以通过模板中的变量获得。 Hugo提供了一些顶级变量来访问内容，包括:
- $—此变量表示模板的顶级上下文。 在页面模板的情况下，此变量表示当前页面。 像标题这样的页面级元数据以$.Title的形式提供，而描述以$.Description的形式提供。 页面级变量通过Page属性链接到自身，因此我们可以将网站的标题写为 $.Page.title。
- site—该变量提供整个网站的数据。 我们可以使用这个变量来访问config.yaml中的配置， 通过site.Pages浏览网站的页面， 使用site.Taxonomies浏览Taxonomy， 并使用site.Params查看定制参数。
- hugo—这个变量提供了对Hugo编译器的访问。 编译器包括诸如hugo.IsProduction(用于检测我们是否为生产而构建)和hugo.Version(用于通知我们关于Hugo版本的信息)之类的方法。

{{< hint info >}}
**Exercise 5.1**

Hugo中的shortcode也允许Go模板。在shortcode中顶级上下文$代表什么？
- a. The shortcode
- b. The containing page
- c. The entire site
- d. None of the above
{{< /hint >}}


前面提供的元数据在页级变量中可用，可通过 $ 或 $.page访问。 此外，页面级变量有多个属性和子属性，我们可以使用它们来访问用户提供的和Hugo生成的有关页面的元数据。 我们可以通过使用页面级变量 $.Title和 $.Description在索引页面 (layouts/ index.html) 的模板中使用这些。 下面的清单提供了页面级变量，我们将使用这些变量填充网站的<head>部分。

{{< details title="Listing 5.2 Using page variables (layouts/index.html)" open=true >}}
```html
<head>
<meta charset="UTF-8">
<meta name="description" content="{{$.Description}} ">
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<link rel="stylesheet" href="./index.css">
<title>{{$.Title}}</title>
</head>
```
{{< /details >}}   

我们可以在索引页的正文中重用页面标题。 这样，我们就不需要在网页上重复这些信息。 下面的清单显示了如何在Hugo模板中多次访问同一参数以重用页面标题。

{{< details title="Listing 5.3 Accessing the same parameter (layouts/index.html)" open=true >}}
```html
<h1>{{$.Title}}</h1>
```
{{< /details >}}

Hugo标准化了网页的标题和描述属性。 这些在顶级页面对象中可用。 自定义元数据项subtitle在Hugo的顶级不可用。 要访问subtitle变量，我们需要在页面中使用Params对象。 这样，参数对象就会保存前面的所有用户定义的元数据。 通过将所有自定义元数据移至Params对象，Hugo团队能够向页面变量添加更多属性，而不会破坏与较旧网站的兼容性。 下面的清单显示了如何访问Params对象中的subtitle变量。

{{< details title="Listing 5.4  Accessing nonstandard parameters (layouts/index.html)" open=true >}}
```html
<h2>{{$.Params.Subtitle}}</h2>
```
{{< /details >}}

{{< hint warning >}}
**NOTE** 尽管我们将元数据项定义为subtitle，但在清单中，我们将其作为subtitle访问。 $.Params中的变量不区分大小写。 提供的标题也存在于Params中，可以作为 $.Params.title访问。
{{< /hint >}}

{{< hint info >}}
**CODE CHECKPOINT**     https://chapter-05-01.hugoinaction.com, and source code: https://github.com/hugoinaction/hugoinaction/tree/chapter-05-01.
{{< /hint >}}

## 5.1.2 存在检查

尽管我们的代码提供了所需的数据，但在某些情况下，代码将失败。 编写标记驱动的网站时的一条经验法则是假设所有属性都是可选的。 这使得所有内容都是可移植的。 如果用户从一个不同的主题切换到一个更新的主题，他们强烈希望网站始终保持正常运行。 他们可以慢慢提供数据来支持特定的功能。 如果我们没有提供任何元数据，那么我们刚刚创建的主页将呈现空字符串，而不是所有的定制数据。 但是我们可以通过提供默认值和运行存在检查来做得更好。

清单5.5提供了一种使用Hugo中的if语句执行存在检查的方法。 在清单中，if语句检查其参数的标题，描述和副标题的真实值。 当提供的参数为true时，if语句执行if块内的模板代码。 此外，如果我们不提供内部内容，则不存在容器HTML标签。 if检查失败的值包括false、0、不存在的变量(nil)、slice、map或string长度为零。

{{< details title="Listing 5.5  Using existence checks (layouts/index.html)" open=true >}}
```html
...
{{if $.Description}}
<meta name="description" content="{{$.Description}}">
{{end}}
...
{{if $.Title}}<title>{{$.Title}}</title>{{end}}
...
{{if $.Title}}<h1>{{$.Title}}</h1>{{end}}
{{if $.Params.Subtitle}}<h2>{{$.Params.Subtitle}}</h2>{{end}}
...
```
{{< /details >}}

{{< hint info >}}
**CODE CHECKPOINT**	https://chapter-05-02.hugoinaction.com, and source code: https://github.com/hugoinaction/hugoinaction/tree/chapter-05-02
{{< /hint >}}

## 5.1.3 将站点变量用于默认值

页面标题也是可选的。 如果我们不提供主页的标题，我们可以回到config.yaml文件中提供的网站标题。 下面的清单显示了如果页面标题不可用，我们如何通过使用内容的site.Title变量来实现这一点。 我们可以使用else逻辑回到site.Title。

{{< details title="Listing 5.6  Falling back to the website’s title (layouts/index.html)" open=true >}}
```html
{{if $.Title}}
<title>{{$.Title}}</title>
{{else if site.Title}}
<title>{{site.Title}}</title>
{{end}}
```
{{< /details >}}

{{< hint info >}}
**CODE CHECKPOINT**	https://chapter-05-03.hugoinaction.com, and source code: https://github.com/hugoinaction/hugoinaction/tree/chapter-05-03.
{{< /hint >}}

我们还可以使用$.Site访问站点变量。 由于站点在Hugo模板中全局可用来访问所有站点变量，因此建议使用site而不是$.Site。 这是因为并不是所有模板类型都可以使用$.site。

## 5.1.4 创建简化变量

尽管主页上需要两次页面标题，但这是不必要的重复。 我们可以将标题存储在名为 $title的变量中，并使用它，如下面的清单所示。

{{< details title="Listing 5.7  Declaring $title with a default value (layouts/index.html)" open=true >}}
```html
{{$title := $.Title}}  Declares a variable called $title
```
{{< /details >}}    

请注意，所有用户定义的变量都以美元符号($)开头。 声明还要求 := 进行赋值。 对于将来的赋值，我们也可以使用单个等号(=)。 如果需要，下面的清单显示了如何为Hugo变量提供后备值。

{{< details title="Listing 5.8  Using if to provide a fallback value (layouts/index.html)" open=true >}}
```html
...
{{if not $title}}
{{$title = site.Title}}
{{end}}
```
{{< /details >}}

在清单中，如果是否，则检查页面标题是否为true，如果是，则将$title变量重置为网站标题。 在Go模板语言中，not是一个布尔函数。 它接受一个参数并反转其真假。

请注意，我们可以使用=重置现有变量，使用:=声明新变量。 Hugo将变量作用范围限定在它们所在的代码块。 换句话说，在if块内声明的变量不能在其外部访问。 因为我们之前用默认值定义了$title，所以我们不需要else语句来匹配上一个清单中的if语句。

还要注意，我们不能在不声明变量的情况下使用它们。 声明失败前使用变量。 因为我们在清单5.7中声明了title变量，所以我们现在可以在任何需要页面标题的地方使用$title作为备用。 下面的清单显示了这种用法。

{{< details title="Listing 5.9  Providing the web page title (layouts/index.html)" open=true >}}
```html
{{if $title}}<title>{{$title}}</title>{{end}}
```
{{< /details >}}   

{{< hint info >}}
**CODE CHECKPOINT**	https://chapter-05-04.hugoinaction.com, and source code: https://github.com/hugoinaction/hugoinaction/tree/chapter-05-04.
{{< /hint >}}

## 5.1.5 使用标准库函数来减少代码

尽管我们没有做任何特别的事情来获得标题，但我们的代码可能会不必要地冗长且难以编写和理解。 Hugo为其网站中的常见代码模式预定义了功能。 这些可以大大降低模板的复杂性及其代码大小。 我们通过使用清单5.8中的not函数体验了Hugo的函数。 接下来让我们看看另一个雨果函数。

如果没有值，我们可以使用默认函数来提供缺省值。 我们可以用默认函数的用法替换if检查。 下面的清单使用default作为快捷方式，为我们的网站提供默认标题。

{{< details title="Listing 5.10  Declaring a default title (layouts/index.html)" open=true >}}
```html
{{$title:= default site.Title $.Title}}
```
{{< /details >}}    

Hugo函数将其参数与空格分开。 函数调用可以用括号包装，()。 除非我们在有歧义的地方使用多个嵌套函数，否则在调用Hugo函数时，括号是可选的。 我们可以在清单5.7中编写不调用，就好像 (not $.Title)， 并且default调用的无括号版本是(default site.Title $.Title)。

默认函数的第一个参数是缺省值，而第二个参数是要检查并使用的值(如果存在)。 default和常规if检查之间的一个区别是default检查值的存在，而if检查值的真假。 空字符串、FALSE和0将无法通过真实性测试。 if语句还将检查else代码块 (如果可用)。 (这仅对字幕字段有效。注意，Hugo将title作为字符串属性提供，并将False强制为字符串“False”，这对于$.Title来说是真的)。 为了使默认行为与if语句匹配，我们应该使用isset函数。 下面的清单使用此函数检查变量是否未定义。

{{< details title="Listing 5.11  Using the isset function (layouts/index.html)" open=true >}}
```html
{{if isset $.Params "subtitle"}}<h2>{{$.Params.subtitle}}</h2>{{end}}
```
{{< /details >}}

如果我们传递false作为网页的副标题 (通过在.md文件的前面设置subtitle: false)，Hugo仍然会呈现网页。

另一个值得一提的函数是$.Param。 此函数与 $ 对象绑定，因为它访问site.Params和 $.Params。 访问页面变量和回退到站点变量的模式非常常见，因此Hugo有一个内置的方法来实现这一点。 我们可以在仅传递subtitle调用以访问标题时使用 $.Param。 下面的清单显示了如何声明$.Param函数来提供subtitle。 $.Param函数提供页面subtitle，如果页面subtitle不存在，则返回到站点subtitle。

{{< details title="Listing 5.12  Using the $.Param function (layouts/index.html)" open=true >}}
```html
{{$.Param "subtitle"}}
```
{{< /details >}}

{{< hint info >}}
**CODE CHECKPOINT**	https://chapter-05-05.hugoinaction.com, and source code: https://github.com/hugoinaction/hugoinaction/tree/chapter-05-05.
{{< /hint >}}

{{< hint info >}}
**Exercise 5.2**

即使某些前置内容属性不存在，继续呈现网站也是一种很好的做法。 ___ 函数允许我们填写一个自定义的回退值，如果front matter条目不存在的话。
{{< /hint >}}

## 5.1.6 通过with条件使用上下文切换来简化进一步的检查

在像site这样的对象中具有深度嵌套的属性。Params使模板变得冗长且难以读取(和写入)。 这种冗长的行为使用户无法正确地对其键进行分组，从而影响了网站的可维护性。 例如，我们提供了site.Params.Footer[0].title作为Eclectic主题的属性。 人们可不想在代码中写这一行五次。 Hugo提供了一个特殊的上下文变量，点(.)来解决这个问题。

上下文变量可以近似理解为面向对象编程语言中的this变量，this指方法所在的对象。 呈现页面时，上下文变量表示页面，但如果我们呈现taxonomy，它就变成了taxonomy。 如果我们呈现shortcode，则上下文变量将变为该shortcode。 在属性的上下文中工作时，我们可以使用该属性覆盖上下文变量，并使用. variable。

Hugo提供了with条件，它覆盖了其代码块中的上下文变量。 使用with，我们可以编写一个不太冗长的存在检查。 这是因为如果变量提供了一个值，则调用其内部代码块。 我们可以将变量或表达式传递给with。 如果它计算为真 (非 nil,0,false或空slice，dictionary或string)，则将该值设置为的值.(点) 在与语句中包含的块内。 如果该值不为true，则跳过with块。 下面的清单显示了如何使用与覆盖上下文变量。 .表示传递给with的变量的值。

{{< details title="Listing 5.13 Overriding the context variable (layouts/index.html)" open=true >}}
{{with $title}}<title>{{.}}</title>{{end}}
{{< /details >}}

在与代码块内部，上下文变量被替换为$title变量的值。 请注意，如果我们不设置$title，则不会执行此代码。 但是，如果我们在与块中提供else代码块，则Hugo会运行该代码。

{{< hint info >}}
**CODE CHECKPOINT**	https://chapter-05-06.hugoinaction.com, and source code: https://github.com/hugoinaction/hugoinaction/tree/chapter-05-06.
{{< /hint >}}

默认情况下，$是顶级上下文变量，但我们可以从代码中删除不必要的$符号，将其转换为典型的Hugo主题开发人员会编写的内容。 仅当我们需要访问with块中的顶级上下文时才需要 $。

{{< hint info >}}
**Exercise 5.3**

在雨果模板中，with应该在什么时候使用？
- a. 与是雨果的 “坏” 部分之一，对性能产生巨大的负面影响，不应使用。
- b. with可用于检查值的存在，并提供缺省行为或缺省值。
- c. 如果仅依赖变量的子属性，则可以使用它来更新上下文以编写更少的代码。
- d. with可用于提供映射属性的内联处理，而不必编写诸如index之类的嵌套函数来访问该属性。
- e. both b and c.
- f. both c and d.
- g. b, c, and d.
{{< /hint >}}

## 5.1.7 添加内容处理

在本节中，我们将使用更多的Hugo特性来增强主页，使其与图5.2中所示的设计相匹配。 到目前为止，我们呈现的subtitle字段是纯文本的。 我们希望以大写字母开始，并提供对subtitle使用基于Markdown的格式的功能。 因为subtitle已经在变量中可用，所以此任务涉及将subtitle传递给适当的函数以进行进一步处理。 要使subtitle以大写字母开头，我们可以将其赋予Humanize函数，如下面的清单所示。

{{< details title="Listing 5.14  Adding the humanize function (layouts/index.html)" open=true >}}
```html
{{with .Param "subtitle"}}<h2>{{humanize .}}</h2>{{end}}
```
{{< /details >}}

在 “humanizing” subtitle之后，我们可以通过markdownify函数将数据通过Markdown解析器来进一步使用Markdown处理。 在第3.1.4节中，我们讨论了主题作者如何从前置数据中解析Markdown；markdown是实现这一目的的函数。 下面的清单显示了如何为将来的Markdown支持添加此功能。

{{< details title="Listing 5.15  Adding the markdownify function (layouts/index.html)" open=true >}}
{{with .Param "subtitle"}}<h2>{{markdownify (humanize .)}}</h2>{{end}}
{{< /details >}}   	

{{< figure src="Figure5.2.svg" title="图5.2 Acme Corporation主页，我们在其中使用了subtitle上的Markdown和标记来控制layout文件夹中的index.html页面" >}}

尽管使用括号调用嵌套函数是一种完全有效的方法，但Hugo也支持pipe operator (|) 以提供更多功能的编程风格。 这允许我们获取前一个函数的输出并将其传递给下一个函数。 下面的清单显示了如何通过管道处理函数。

{{< details title="Listing 5.16  Using the pipe operator (layouts/index.html)" open=true >}}
```html
{{with .Param "subtitle"}}<h2>{{. | humanize | markdownify}}</h2>{{end}}
```
{{< /details >}}

函数式编程风格的方法更易于阅读，并且在函数只接受一个参数时更受欢迎。 我们将以此为契机，通过用双星 (**) 包装它们，使副标题中的 “world” 和 “live in” 为粗体，如下面的清单所示。 我们还需要使用索引页前面的Explore选项链接Explore按钮，以使该页面数据驱动。

{{< details title="Listing 5.17  Highlighting parts of the subtitle (content/_index.md)" open=true >}}
![Listing5.17](Listing5.17.svg)
{{< /details >}}    

Hugo中的ref函数取一个文件或文件夹名，并提供此内容的对应URL。 我们还可以将relref用于相对路径。 下面的清单调用ref函数将文件转换为相应的URL。

{{< details title="Listing 5.18  Using the ref function (layouts/index.html)" open=true >}}
```html
<a href="{{ref . (.Param "explore")}}"
>Explore</a>
```
{{< /details >}}

{{< hint info >}}
**CODE CHECKPOINT**	https://chapter-05-07.hugoinaction.com, and source code: https://github.com/hugoinaction/hugoinaction/tree/chapter-05-07.
{{< /hint >}}

## 5.1.8 添加Markdown内容

我们在内容文件中有Markdown内容。 可以通过根上下文($)变量上的.Content变量以其HTML形式获得该内容。 我们可以使用模板中的 {{.Content}} 将其放置在页面上的任何位置，以启用主页上的新部分，如图5.3所示。

{{< figure src="Figure5.3.svg" title="图5.3将Markdown内容添加到主页。 about图片来自(安吉拉·彭切娃 (Angela Pencheva) 在Unsplash上的照片; contact图片来自克里斯托弗·杰西基恩 (Cristofer Jeschkeon) 在Unsplash上的照片。)" >}}

让我们将一些Markdown数据添加到Acme公司网站的主页(https://github.com/hugoinaction/hugoinaction/tree/chapter-05-resources/03).  下面的清单提供了索引页面的数据。

{{< details title="Listing 5.19 Adding descriptive content in Markdown (content/_index.md)" open=true >}}
```markdown
Acme is the **best**
==================

![about us](about.jpg) The finest in this field

Acme Corporation&trade; is the _ world's leading manufacturer of digital shapes_. From squares and circles to triangles and
hexagons, we have it all. Browse through our collection of various forms with different thicknesses and line styles.

[About Us](./about)

* * *

![contact us](contact.jpg) Personalized especially for you

We convert dreams into designs. Our artists are one of a kind.
We provide full support for customizing your designs with multiple contact sessions to understand your problems and get a satisfying result.

[Talk to us today](./contact)
```
{{< /details >}}

要使用此内容，我们还需要两个图像，分别是contact.jpg和about.jpg，它们可以放在Content文件夹中用于网站索引的页面包中。 为了适合当前网站的设计，我们将在当前部分中添加ID介绍，并在Markdown内容中创建一个带有ID描述的新部分。 下面的清单显示了如何做到这一点。

{{< details title="Listing 5.20 Rendering the Markdown content (layouts/index.html)" open=true >}}
```html
<section id="intro">
...
</section>
<section id="description">
{{.Content}}
</section>
```
{{< /details >}}

{{< hint info >}}
**CODE CHECKPOINT**	https://chapter-05-08.hugoinaction.com, and source code: https://github.com/hugoinaction/hugoinaction/tree/chapter-05-08.
{{< /hint >}}

Hugo通过Markdown解析器自动运行Markdown文件中提供的此内容，并提供一个HTML字符串直接放置在文档中。

{{< hint info >}}
**定制从Markdown生成的HTML**

在从Markdown生成HTML的同时，Hugo为开发人员提供了自定义针对特定元素生成的HTML的灵活性。 称为渲染挂钩模板的特殊模板可以精确控制渲染的发生方式。 例如，我们可以在layouts/_default/_markup/render-image.html、layouts/_default/_markup/render-link.html或layouts/_default/_markup/ render-heading.html使用自定义模板， 然后决定如何呈现Markdown中提供的内联图像、链接和标题。

这些模板可以访问整个页面和站点变量集， 以及唯一变量，如.Level、.Text、.Title、 和HTML标题的.Destination，显示文本，附加标题， 和在Markdown中提供的URL。 在第6章中，我们将创建自定义渲染挂钩来控制Markdown渲染。

请注意，_default文件夹中的模板适用于整个网站。 通过将这些模板移动到特定的内容类型，我们可以将这些模板限制在一组页面中。 我们将在第7章讨论内容类型。 开发人员可以使用findRE(译注：findReplace)之类的方法进一步处理生成的HTML字符串，以替换某些子字符串。
{{< /hint >}}