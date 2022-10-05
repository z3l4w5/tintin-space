---
weight: 1
title: "6.1 使用内容类型、基本模板和块来构建模板结构"
date: 2022-09-12T18:26:30+08:00
draft: true
---

# 6.1 使用内容类型、基本模板和块来构建模板结构

到目前为止，我们一直专注于使用Go模板语言为主页创建index.html。 虽然我们还没有一个很大且无法管理的文件，但如果我们不断向该文件添加代码，它可能很快就会失控。 另外，对于一个文件，我们无法在略有不同的各种网页之间共享模板代码。

在本节中，我们将开始为索引页面之外的辅助功能构建模板。 在制作新的模板系统时，尽管有两种模板设计，但我们仍将拥有一个功能正常的网站: 一个是Eclectic的，另一个是我们并行建造的。 我们将缓慢地将网站迁移到新代码，以确保最小的破损。 为此，我们将使用正在构建的所有定制模板代码创建一个新的内容类型，并允许页面在Eclectic模板和新模板之间切换。 然后，我们将使用使用Terms作为示例页，为索引页和数据页之间的可重用部分创建代码共享的基本布局，以迁移到新的内容类型。

## 6.1.1 封装具有不同内容类型的模板

Hugo内容类型是模板的集合，可以根据独特的设计从标记中呈现页面。 从概念上讲，内容类型类似于主题，但内容类型不是整个网站的设计，而是只呈现给部分。 每个网站可以有多种内容类型，每种内容类型可以不同地显示内容。 例如，在一个典型的网站中，我们可以有一个与新闻帖子相关联的页面和一个不同的博客帖子页面的设计，还有另一个隐私策略页面的设计。 我们可以用不同的内容类型对每种类型的页面 (博客、新闻、一般文本等) 进行建模。 每种内容类型都可以有一个独立的呈现模板。

主题是链接到网站不同部分的多种内容类型的集合。 并不是网站中的所有页面都需要看起来完全相似，而内容类型也允许这种多样性。 每个主题都定义了所有页面恢复到的默认类型，除非它们为网站内的各个部分使用由主题定义的自定义内容类型。 通过在布局目录中放置一个名为index.html的文件，我们可以覆盖主题定义的默认类型的索引模板。 Hugo支持通过在主题中存在的布局目录中的确切位置创建文件来覆盖主题中的任何模板。 Hugo将所有代码路径重定向到新文件。

除非我们研究主题内部并确保我们没有破坏任何代码路径的渲染， 在某个地方很有可能导致意外的行为。 我们应该避免直接覆盖模板，除非我们正在对主题进行小错误修复。 将模板更改放在不干扰主题的新内容类型中要安全得多。 然后，我们可以将所有页面慢慢移动到该类型，并在页面不再使用主题时将其从网站上停用。 这种方法允许我们逐渐地从一个主题移动到另一个主题或定制代码(就像我们正在做的那样)，从而实现更多的控制。 新的内容类型为不同于主题的基于标记的内容定义了一种新的呈现类型。

在向网站添加更多模板代码之前，我们将创建一个新的content type来隔离我们的更改。 我们可以为主题未使用的content type选择任何名称，以防止冲突。 我们将该内容类型命名为Modem(用于现代设计)，并将索引页移动到该类型定义。 为了执行此任务,让我们在layouts目录中创建一个名为modern的文件夹，并将index.html移动到该文件夹。 接下来，在主页的索引文件中，即content/_index.md中，我们将把类型更新为modern，如下面的清单所示。

{{< details title="Listing 6.1 Updating the content type (content/_index.md)" open=true >}}
```markdown
type: modern
```
{{< /details >}}

{{< hint warning >}}
**NOTE** Hugo使用主题提供的默认模板来渲染索引页的内容，除非存在类型字段。
{{< /hint >}}

{{< hint info >}}
**CODE CHECKPOINT**  https://chapter-06-01.hugoinaction.com, and source code: https://github.com/hugoinaction/hugoinaction/tree/chapter-06-01.
{{< /hint >}}

{{< hint info >}}
**雨果巧妙的模板查找顺序**

Hugo巧妙地根据网站开发者的意图分配一个合适的模板。 例如，如果我们在content目录中创建了一个名为blog的文件夹，则Hugo会将该文件夹中所有文件的内容类型设置为blog。 然后，如果我们在layouts文件夹中创建一个名为blog的文件夹，并开始为这些页面定义模板， 他们会自动被网站上的博客栏目选中。 另一方面，如果未指定此类内容类型，则会自动加载默认模板。

通过在Hugo中设计良好的模板查找顺序，这种content type选择成为可能。 当Hugo需要呈现页面时，它会经过一个有序的文件列表，并执行第一个文件作为网页的模板。 由于向后兼容性，这个列表很大，并且它提供了许多命名模板文件的方法。 但是，我们强烈建议你在代码中使用直接的类型到文件夹约定，并使用前面的类型字段进行手动覆盖。 雨果的网站在https://gohugo.io/templates/lookup-order/上提供了模板查找顺序
{{< /hint >}}

## 6.1.2 提供基础模板以供重用

Most web pages have a similar HTML structure. 有一个带有元数据的head部分以及页眉，主和页脚，它们定义了整个网站中页眉和页脚所在的界面。 Hugo有一个基本模板的概念，它可以包含在整个网站上共享的这些公共元素。 基础模板持有网站的骨架。 它包含网页常见部分的默认HTML，如果需要，可以在特殊情况下覆盖它。 类型中的所有模板都可以继承并自定义该类型的基础模板。 如果一个类型没有提供基本模板，我们可以使用整个网站的默认基本模板。

Hugo中的base模版被命名为baseof.html。 让我们在modern文件夹中创建一个基本的basof.html文件。 此文件存储了Acme Corporation网页框架，我们将在使用modern类型的所有页面中使用该框架。 通过创建basof.html，我们切断了与Eecectic提供的模板的联系，可以专注于我们的定制主题。

## 6.1.3 定义代码块

让我们在基本文件base of.html中创建一个框架。 索引页中的 <head> 标记不是特定于主页的，因此我们可以将其移动到基础模板。 <body>标记中的内容是特定于页面的，我们将把它保留在指定的index.html模板中。 然后，在baseof.html中，我们将放置基础模板 (https://github.com/hugoinaction/hugoinaction/tree/chapter-06-resources/01)。

块定义了我们可以在专用模板中覆盖的内容。 基础模板将块用于可以被子模板覆盖的内容。 我们可以为非覆盖模板提供默认值。 如果特定页面使用的模板未覆盖此块，则Hugo会在基本模板的块内执行代码。 我们可以在模板中包含任意数量的块，包括嵌套块。 下面的清单显示了在Hugo中创建块的语法。

{{< details title="Listing 6.2  Understanding a block in Hugo (don’t add this to your website)" open=true >}}
```html
<!-- Block creation -->
<!-- In baseof.html -->
{{block "blockname" blockArgument}}
{{end}}

<!-- In derived template -->
{{define "blockname"}}
<!-- The dot (.) refers to the supplied block argument here -->
<!-- We can still access $ if we need the top-level template (page) variable access -->
{{end}}
```
{{< /details >}}

该块有两个参数：块的名称和要传递给块的上下文变量。 传递上下文变量的值替换的值。在街区里。 我们将为基本模板中的块提供当前上下文(也是全局上下文$)。

当我们添加块以允许覆盖模板的可自定义部分时，我们还需要确保从基本模板派生的页面可以从所有url正确加载。 在清单6.3中，我们将URL更改为index.css，并将其基于网站基本URL，而不是相对于当前页面的URL。 请注意，基础模板应尽可能通用，以处理特定类型中的所有内容。 还要注意，所有块都应该有合理的缺省值，并且所有参数都应该是可选的。

{{< details title="Listing 6.3  Adding the content type base file (layouts/modern/baseof.html)" open=true >}}
![Listing6.3](Listing6.3.svg)
{{< /details >}}   

在基础模板中，顶层上下文是指当前页面。 所有页面类型都有标题和描述属性。 但是，这些仍然可能是不确定的，因此我们需要检查它们。 属性中添加一个默认值。总结如果。描述不可用。 因为页面可以位于任何位置，所以我们将网站的绝对基础URL用于CSS文件。

BLOCK语句用于定义可在子模板中重写的块。 我们为基础模板中的块提供默认内容，以便如果我们创建一个新模板，即使所有块都没有被覆盖，它也会提供有意义的渲染。 BLOCK语句的最后一个参数类似于WITH语句，它成为块的上下文变量。 在清单6.3中，我们将当前上下文传递给block，而不是隐藏任何信息。 请注意，$TITLE不能在块内工作，根据提供的上下文，块需要是自包含的。

{{< hint info >}}
**Exercise 6.1**

持有HTML骨架的Hugo网站中的根模板称为 _________
- a. root.html
- b. base.html
- c. baseof.html
- d. primary.html
- e. index.html
- f. parent.html
{{< /hint >}}

清单6.3中的代码与从我们的索引页提取的头部分几乎相同。 在index.html页面上，我们现在可以使用清单6.4所示的define关键字来填写block的值。 当我们使用定义时，我们通知Hugo模板定义了基本模板中的块。 如果模板内没有定义，雨果将不会使用基础模板。 还要注意，需要重新定义$TITLE才能在正文中使用。

{{< details title="Listing 6.4  Filling in the block values (layouts/modern/index.html)" open=true >}}
```
{{define "body"}} 
<!-- Redefines $title -->
{{$title := ...}} 
...Contents of the body tag...
{{end}}
```
{{< /details >}}    

{{< hint info >}}
**CODE CHECKPOINT**	https://chapter-06-02.hugoinaction.com, and source code: https://github.com/hugoinaction/hugoinaction/tree/chapter-06-02.
{{< /hint >}}

在前面的清单中，我们在基础模板中定义了主体块。 上下文变量.由基本模板提供。 当我们使用define关键字时，不使用基础模板中块的默认实现。 索引页现在看起来应该和以前完全一样，但是Hugo是由两个文件组成的，而不是一个文件--来自基本模板和索引模板。

## 6.1.4 在不同布局中重复使用基础模板

有了基本模板，代码就可以在其他页面上重复使用了。 我们使用index.html来表示网站的索引页。 “index” 这个名字不是随机的。 Hugo开发人员选择这意味着整个网站的主页，而在日常的Web开发中，索引文件代表特定部分(或文件夹)的主页。 在Hugo布局中，它始终表示网站的主页。 在Hugo中，我们呈现的各种类型的页面称为布局。 雨果支持的布局主要有四种:
- 列表布局呈现网站内各部分的索引页。 这通常提供所有小节的列表和节内所有页面的列表。 呈现每个分支捆绑包(_index.html)的基本页面使用列表布局。
- 单个布局表示常规网页，其内容存储在标记文档或叶束中。 所有叶捆绑包(index.md)和纯Markdown文档(mypage.md)都使用单一布局。
- 索引布局呈现整个网站的主页，该主页存在于网站的根目录中。 此布局是列表布局的专门化，之所以出现，是因为主页通常不同于部分列表页。 如果缺少索引布局，则Hugo将列表布局用于网站的主页。
- 404布局构成网站内所有错误页面的基础。 此布局将创建一个唯一的页面 (/404.html)，我们可以在托管服务器上为未找到页面 (HTTP 404) 错误进行配置。 我们可以自由地为503服务器错误创建更多的错误页面，如503.html，尽管使用JAMSTACK的静态托管，发生500系列错误的机会很低。 许多开发人员不需要任何超出404的页面。

除此之外，我们还有两个布局：taxonomy和terms。 这些分别用于呈现terms列表 (例如，标签列表) 和与所述terms相关联的页面列表 (例如，标记为square的页面列表)。 这些布局通常可以重复使用我们为列表布局所做的大部分工作。(我们将在第7章中更详细地讨论这些问题。)列表和单个布局是Hugo中最关键的布局，分别对应于leaf和bundle。
让我们为网站中的单个页面添加singlele.html。 我们可以在这里添加特定于单个页面的代码。 在acme Corporation网站的single.html中，我们不想覆盖基本模板，而是按原准则使用基本模板的内容。 如果模板不是以定义的块开始，Hugo会将模板视为整个网页。 如果我们将页面留空而不是运行基本模板，则Hugo会呈现一个空页面。 要通知Hugo加载基本模板，我们需要定义一个不会使用的虚拟块。 下面的清单显示了如何做到这一点。

{{< details title="Listing 6.5 Adding dummy content to single.html (layouts/modern/single.html)" open=true >}}
```
{{define "garbage"}}
<!-- Never gets rendered -->
{{end}}
```
{{< /details >}}

请注意，如果我们将注释放在定义块之外，这将不起作用。 它将失败，因为在覆盖模板部分的模板中只允许定义块。

接下来，我们将此模板分配给使用Term页面。 在terms.md中，我们将在前面添加type:modern来执行此分配，然后将其转换为图6.2所示的设计。 使用Terms页的内容现在使用

{{< figure src="Figure6.2.svg" title="图6.2使用在Acme类型中创建的single.html模板呈现的使用条款页面" >}}

主页的css，没有提供良好的格式设置。 清单6.6显示了如何添加特定于布局的类覆盖。 我们将在basof.html中的Body标记中执行此操作。

{{< details title="Listing 6.6  Adding support for a class override (layouts/modern/baseof.html)" open=true >}}
```
<!-- There’s no need to escape quotes within the block. -->
<body class="{{block "bodyClass" .}}{{end}}">
```
{{< /details >}}    

我们可以在模板中任意位置使用代码块。 它们执行简单的字符串替换，并不关心我们网页的HTML结构。 因此，如果我们在某些标签中放置错误的HTML (例如，bodyClass中的引号)，则输出可能会被破坏。 请注意，模板会自动对来自标记文档的特殊字符进行XML编码，因此，我们可以将它们添加到HTML标记属性中，而无需额外的编码。 下面的两个清单显示了如何在index.html和single.html中覆盖bodyClass，以迎合这一点。 请注意，在将适当的定义添加到单个页面(清单6.8)之后，我们可以删除虚拟定义“垃圾”(来自清单6.5)。

{{< details title="Listing 6.7  Defining a home page with home (layouts/modern/index.html)" open=true >}}
```html
{{define "bodyClass"}} home {{end}}
```
{{< /details >}}

{{< details title="Listing 6.8  Defining a regular page with page (layouts/modern/single.html)" open=true >}}
```html
{{define "bodyClass"}} page {{end}}
```
{{< /details >}}

{{< hint info >}}
**CODE CHECKPOINT**	https://chapter-06-03.hugoinaction.com, and source code: https://github.com/hugoinaction/hugoinaction/tree/chapter-06-03.
{{< /hint >}}

{{< hint info >}}
**Exercise 6.2**

Hugo用于常规网页的布局存储在名为 ______ 的文件中。
{{< /hint >}}

我们可以在单个文件中根据需要定义任意多个覆盖。 Hugo不检查最终HTML的有效性。 我们应该确保不会因为覆盖的内容而导致无效的HTML。 在我们的示例中，在class属性bodyClass中使用quote (“) 关闭该属性并产生意外结果。

我们的使用terms页面仍然不完整。 我们在主页上有一个页眉和一个页脚，准备移动到基础模板。 执行此操作时，我们应始终创建一个新块，以便根据需要进行覆盖。 我们将通过使图像路径为绝对的方式来概括代码以满足所有页面的需求，从而允许其在任何子页面中使用。 下面的清单将页眉和页脚移动到基本模板，以便在所有页面之间共享。

{{< details title="Listing 6.9  Moving the header and footer (layouts/modern/baseof.html)" open=true >}}
![Listing6.9](Listing6.9.svg)
{{< /details >}}

{{< hint info >}}
**CODE CHECKPOINT**	https://chapter-06-04.hugoinaction.com, and source code: https://github.com/hugoinaction/hugoinaction/tree/chapter-06-04.
{{< /hint >}}

通过这些更改，索引页面模板现在只有特定于该页面的内容， 我们可以在其他地方使用的共享部分，如页眉和页脚，已经移到了共享模板中。 使用条款页面看起来像一个完整的网页。 然而，我们会回到主页来进一步改进它。