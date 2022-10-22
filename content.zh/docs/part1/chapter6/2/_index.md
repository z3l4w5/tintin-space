---
weight: 2
title: "6.2 用partials重用内容"
date: 2022-09-12T18:26:30+08:00
draft: true
---

# 6.2 用partials重用内容

当我们在主页上引入新部分时，它将页脚菜单向下推，远离网站顶部。 虽然这些链接不像标题那么重要，但我们希望在不滚动的情况下提供它们(通常称为上方折叠，来自报纸，在报纸上，隐藏在首页折叠下的文章被认为不那么重要)。 理想情况下，我们希望重用代码来控制页脚。

由基本模板和代码块提供的继承(模板获取或继承基本模板的整个代码，并有权修改或更改某些部分)不适合在网页上的任意位置重复使用代码。 为此，我们需要组件化，在那里我们有一个可重用的模板代码，我们可以插入任何我们想要的地方。 我们可以使用shortcodes来共享标记数据中的共享功能片段，也可以使用partials来共享模板中的公共代码片段。

Partials是标准编程语言中的函数等价物，它支持隔离一段计算，该计算生成一些输出到渲染的HTML文件并返回一些数据。 Partials接受参数，使用这些参数进行一些处理，并将数据记录到输出的HTML文件中，将计算结果返回给调用者。 Partials是Hugo最重要的模板功能之一，了解partials的概念对于与Hugo取得成功至关重要。 表6.1 比较了使用partials和使用基本模板代码进行重用的情况。

表6.1 Partials与基于基础模板的代码重用

![Table6.1](Table6.1.svg)

## 6.2.1 移动到partials

让我们从将页脚菜单移动到partials开始。 为此，我们将创建一个名为layout/partials/menu.html的文件，并移动代码以生成指向该文件的主页上使用的基于菜单的链接。 请注意，我们没有在布局下使用modern子文件夹。 在Hugo中的所有内容类型中都可以使用partials。 此外，我们可以在本地覆盖主题中使用的partials，并通过在layouts/partials文件夹中创建一个具有相同名称的文件来更改其行为。

Partials覆盖允许我们替换与主题一起使用的页面的部分，并自定义这些部分。 partials文件夹允许将子文件夹用作名称空间， 虽然我们现在不需要(https://github.com/hugoinaction/hugoinaction/tree/chapter-06-resources/02). 下面的清单显示了如何共享我们的代码以从partials创建页脚菜单。

{{< details title="Listing 6.10  Sharing the code via a partial (layouts/partials/menu.html)" open=true >}}
```html
{{with site.Menus.footer }}
<nav>
    <ul>
    {{range .}}
    <li>
        <a href="{{.URL}}">{{.Name | humanize}}</a>
    </li>
    {{end}}
    </ul>
</nav>
{{end}}
```
{{< /details >}}

要调用Partial，我们使用Partial语句，后跟名称和上下文变量。 下面的清单使用此语句将页脚菜单添加到index页的hero部分。

{{< details title="Listing 6.11 Calling a partial (layouts/modern/index.html)" open=true >}}
```html
<section id="intro">
...
{{ partial "menu.html" . }}
</section>
```
{{< /details >}}

就像块语句一样，partial语句也需要传递一个上下文变量。 传递上下文变量用于加载menu.html，所以我们可以在页脚中重用它。 下一个清单提供了这方面的代码。

{{< details title="Listing 6.12  Reusing the footer menu (layouts/modern/baseof.html)" open=true >}}
```html
{{block "footer" .}}

<footer class="dark">
{{ partial "menu.html" . }}
...
</footer>
{{end}}
```
{{< /details >}}

{{< hint info >}}
**CODE CHECKPOINT**	https://chapter-06-05.hugoinaction.com, and source code: https://github.com/hugoinaction/hugoinaction/tree/chapter-06-05.
{{< /hint >}}

## 6.2.2 partial上下文

Hugo的Partials是自治独立的，除了传递给它们的变量之外，没有其它变量。 Partial内的$变量并不引用全局页面对象，而是传递给Partial的顶级上下文变量。 虽然我们可以将整个顶层上下文从调用者传递到partials，但最好限制这些数据。 这一限制通过以更好的方式缓存来确保最大限度地重用部分和性能优化。 否则，我们会将太多的信息传递给部分，远远超过所需的信息。

如果我们直接传递菜单，我们可以重复使用页脚和主菜单之间的partials。 在下面的清单中，我们更新了部分菜单以呈现特定的菜单，而不是网站的硬编码主菜单，从而使其能够呈现不同的菜单。

{{< details title="Listing 6.13  Making the partial more flexible (layouts/partials/menu.html)" open=true >}}
![Listing6.13](Listing6.13.svg)
{{< /details >}}

We can reuse the previous listing using the code in the footer menu. The following listing shows this use.

{{< details title="Listing 6.14 Loading the footer menu (layouts/modern/baseof.html)" open=true >}}
{{ partial "menu.html" site.Menus.footer }}
{{< /details >}}

{{< hint info >}}
**CODE CHECKPOINT**	https://chapter-06-06.hugoinaction.com, and source code: https://github.com/hugoinaction/hugoinaction/tree/chapter-06-06.
{{< /hint >}}

Hugo中的partial语句在概念上类似于JavaScript模块或PHP include。 现在我们可以使用 {{ partial "menu.html" site.Menumes.main }} 作为主菜单的参数，并且 {{ partial "menu.html" site.Menumes.footer }} 会呈现页脚。

将主菜单移动到部分菜单的一个问题是丢失了用于在移动设备上呈现主菜单的hamburger按钮。 因为到处都不需要它，所以我们需要将其它参数传递给部分，以弄清楚何时呈现此按钮。

Hugo Partial只有一个参数。 为了允许传递多个值，我们可以将该参数转换为具有多个值的字典或slice。 slice会导致可读性问题，因为参数的顺序变得很重要，而且很难支持未定义的参数。 为了避免这些问题，下面的清单使用字典参数作为菜单的可选元素，以重新使用header的partial。

{{< details title="Listing 6.15 Adding the hamburger button (layouts/partials/menu.html)" open=true >}}
{{with $.Menu }}
<nav>
{{if $.Button}}
<button class="hamburger">☰</button>
{{end}}
<ul>
{{ range $.Menu }}
<li><a href="{{.URL}}">{{.Name | humanize}}</a></li>
{{end}}
</ul>
</nav>
{{ end }}
{{< /details >}}    	

现在，我们可以使用PARTIAL并为按钮选项传递TRUE来加载带有汉堡按钮的标题菜单。 下面的清单提供了这方面的代码。 请注意，我们不需要在页脚中传递Button参数，因为默认值将无法通过If检查。

{{< details title="Listing 6.16 Loading the header menu (layouts/modern/baseof.html)" open=true >}}
```
{{ partial "menu.html"
(dict "Menu" site.Menus.main "Button" true)
}}
```
{{< /details >}}

{{< hint info >}}
**CODE CHECKPOINT**	https://chapter-06-07.hugoinaction.com, and source code: https://github.com/hugoinaction/hugoinaction/tree/chapter-06-07.
{{< /hint >}}

## 6.2.3 使用附加参数将子菜单带回到菜单部分

当我们移动到我们的内容类型时，我们丢失了header中的子菜单。 现在是把它带回来的好时机。 Hugo支持在树形数据结构中无限嵌套子菜单，并使用父子术语分别表示菜单及其子菜单。 每个菜单对象都有一个名为called的属性。有一个名为Child的切片(数组)，我们可以使用它来呈现这些对象。 下面的清单将子菜单添加为部分菜单中的嵌套无序列表。 对于页脚这样没有子菜单的情况，此调用没有任何影响。

{{< details title="Listing 6.17  Submenus as nested unordered lists (layouts/partials/menu.html)" open=true >}}
```html
<li>
<a href="{{.URL}}">{{.Name | humanize}}</a>
{{if .HasChildren}}
<ul>
{{ range .Children }}
<li><a href="{{.URL}}">{{.Name | humanize}}</a></li>
{{ end }}
</ul>
{{end}}
</li>
```
{{< /details >}}

{{< hint info >}}
**CODE CHECKPOINT**	https://chapter-06-08.hugoinaction.com, and source code: https://github.com/hugoinaction/hugoinaction/tree/chapter-06-08.
{{< /hint >}}

Hugo的菜单对象提供了其它功能，例如当我们在正确的页面上时突出显示活动菜单。 这些扩展超出了本书的范围。 此外，Hugo的文档提供了一个现成的菜单模板，该模板涵盖了比我们在此处的代码所能提供的更多案例。

## 6.2.4 Partials与性能

当模板存在于多个页面中时，每个页面都会进行一次模板调用。 在许多页面上，这可能会减慢网站的编译速度。 Partials允许我们执行缓存以防止重复调用。 在使用此功能之前，让我们花几分钟时间了解一下我们刚刚编写的代码的性能。

Hugo提供了一个区分大小写的构建标志 -- templateMetrics。 当使用该参数时，它测量每个模板对整体构建的影响。 请注意，许多Hugo操作是并行运行的。 因此，提供的所有时间的总和远远超过编制网站所需的时间。 清单6.18中的代码在Acme Corporation网站上运行性能指标。 请注意，这些数字高度依赖于运行的硬件和软件，并且可能并不总是相同的。 (Hugo及其主题不断发展以提高性能，这些数字可能会发生巨大变化。) 我们刚刚创建的文件menu.html已经运行了四次。

{{< details title="Listing 6.18 Running a performance metrics measurement" open=true >}}
![Listing6.18](Listing6.18.svg)
{{< /details >}}    

清单6.18中要注意的键列是计数列。 Single Page模板(_Default/Single.html)被调用16次以呈现16个页面。 shortcodes单独报告。 菜单部分(artials/menu.html)已经调用菜单模板五次来呈现主页和Terms页。 让我们将隐私策略页面也移动到modern模板类型。 这个menu.html文件被调用了七次，为这个新页面的页眉和页脚分别添加了一次。

{{< hint info >}}
**CODE CHECKPOINT**	https://chapter-06-09.hugoinaction.com, and source code: https://github.com/hugoinaction/hugoinaction/tree/chapter-06-09.
{{< /hint >}}

为了防止这种重复，我们可以使用partialCached而不是partial。 至少，artialCached采用与Partial相同的参数。 如果我们用partialCached替换所有partial调用，而不传递另一个参数，我们会看到partials/menu.html只执行一次。 这种执行是一个明显的错误，因为它强制页眉和页脚具有相同的菜单。

{{< hint info >}}
**CODE CHECKPOINT**	https://chapter-06-10.hugoinaction.com, and source code: https://github.com/hugoinaction/hugoinaction/tree/chapter-06-10.
{{< /hint >}}

为了确保页眉和页脚有自己的菜单，partialCached可以采用任意数量的参数，每个参数都组合在一起以创建一个唯一的键。 我们需要向artialCached添加单独的参数，每个呈现一个参数。 清单6.19将参数添加到索引页。 然后，清单6.20将参数添加到基本模板文件baseof.html。

{{< figure src="Figure6.3.svg" title="图6.3 一切都在线上: Jamstack取得了重大突破，但Alex必须将其保持在线上，导致其声誉受到威胁。" >}}

{{< details title="Listing 6.19  Using partialCached in layouts/modern/index.html" open=true >}}
```html
{{ partialCached "menu.html" (dict "Menu" site.Menus.footer) "footer"}}
```
{{< /details >}}   	

{{< details title="Listing 6.20   Using partialCached in layouts/modern/baseof.html" open=true >}}
```html
{{ partialCached "menu.html" (dict "Menu" site.Menus.main "Button" true)
➥ "main" }}
{{ partialCached "menu.html" (dict "Menu" site.Menus.footer) "footer"}}
```
{{< /details >}}
   	
我们本可以将true作为缓存键添加到Main旁边，但这是不必要的。 那是因为主菜单总是有一个按钮，并且主键足够独特。

{{< hint info >}}
**CODE CHECKPOINT**    https://chapter-06-11.hugoinaction.com, and source code: https://github.com/hugoinaction/hugoinaction/tree/chapter-06-11.
{{< /hint >}}

现在，当我们添加页面时，部分执行的计数不会增加。 Partials采用单个参数 (可以是具有多个值的字典对象dict) 来确保独立性。 这允许高效的缓存。 可以轻松地将partialCached中的其它参数添加到partials中，而无需更改partial代码。

{{< hint info >}}
**TIP** 减少模板所用时间的最简单方法是将一些实现转移到partial，并使用artialCached来处理跨页面相同的较慢的HTML。
{{< /hint >}}

## 6.2.5 绕道到partial的返回

在引入partial时，如果没有提到return语句，仅对对Partial函数的理解了一半。 到目前为止，我们已经在模板文件中使用了partials作为ShortCode的等效项。 虽然在HTML中呈现是部分缓存和部分缓存的一个重要用例，但partialCached也充当Go模板语言中的函数。 我们可以使用partials进行字符串和数字处理，或者访问网络或文件系统，然后在变量中提供处理后的结果。 Partials已经支持通过partialCached进行缓存。

{{< hint info >}}
**Exercise 6.3**

是非题: 基本模板中的块只由Hugo执行一次，并且输出在多个页面之间共享。
{{< /hint >}}

对于本章，让我们在第5章中创建的价格shortcode更快地执行。 价格shortcode读取一个CSV文件，该文件提供任何Acme Corporation产品的价格。 我们将所有产品的价格缓存在一个可在所有页面上访问的partial (https://github.com/hugoinaction/hugoinaction/tree/chapter-06-resources/03)中。 这样，CSV文件的读取和解析只发生一次。

因为表格是二维的，所以我们可以创建字典来表示它。 外部词典将产品名称(行标题)作为关键字，并将产品信息作为其值。 内部字典使用列标题作为键，产品的价格和评级作为值。 下面的清单以JSON格式提供了该函数的输出示例。

{{< details title="Listing 6.21  Output from the price shortcode" open=true >}}
```json	
{
"Circle": {
"Colors": "Red, Green, Blue, Orange", "Price": "2",
"Rating": 4
},
"Square": {
"Colors": "Red, Pink, Blue",
"Price": "4",
"Rating": 5
}
}
```
{{< /details >}}    

Hugo的slice和dict数据结构是不可变的，不能修改。 因此，我们将对此部分使用临时数据结构。 Hugo的scratch结构是一种读写数据存储，可以充当临时变量来保存数据。 它的工作原理就像一个可变字典，我们可以在其中轻松地添加或删除值。 清单6.22创建一个部分，以便从CSV文件中获取产品信息，然后可以对其进行解析和缓存。

{{< details title="Listing 6.22 A partial for product info (layouts/partials/products.html)" open=true >}}
![Listing6.22](Listing6.22.svg)
{{< /details >}}   

该清单中的partial不使用外部变量。 无论参数如何，它都会返回相同的结果，并且对于不同的输入，我们不需要不同的变体。 请注意，在Hugo中，一个partial中只允许一个返回。 此外，当在便笺中创建指向另一个字典的字典时， 外部词典使用行($r)中的第一项作为索引，其值是使用每列($index)中的第一个条目作为键的词典。 现在我们可以更新价格shortcode来利用这个部分。 下面的清单显示了如何做到这一点。 请注意，partialCached至少需要一个键。

{{< details title="Listing 6.23 Using a products partial (layouts/shortcodes/price.html)" open=true >}}
```html
{{$product := default (.Get 0) (.Get "product")}}
$ {{index (index (partialCached "products.html" "key") $product) "Price" }}
```
{{< /details >}}

{{< hint info >}}
**CODE CHECKPOINT**	https://chapter-06-12.hugoinaction.com, and source code: https://github.com/hugoinaction/hugoinaction/tree/chapter-06-12.
{{< /hint >}}

在前面清单中的代码中，我们使用传递给shortcode的参数获得了产品信息。 我们使用partialCached来调用缓存的partial命名产品。 我们给它一个字符串作为参数，因为它不需要变量。 在partial内部，我们创建了一个scratch，其中以键为产品名称，以值为价格。 我们可以使用Hugo提供的模板度量来验证Partial只执行一次。 表6.2比较了partial代码和ShortCode及其在Hugo中的使用。

表6.2 partial和shortcode的比较及其在Hugo中的使用
![Table6.2](Table6.2.svg)

{{< hint info >}}
**内联partials**

Hugo还支持内联定义partial。 如果我们想在同一文件中多次重用相同的代码，但又不想生成单独的文件，则内联部分可以派上用场。 内联partial也可以作为私有函数，而常规部分则作为公共函数。 我们还可以使用define关键字来定义一个块，该块又定义了一个partial。 下面的代码显示了如何实现这些不同的声明。

```
{{ $variable := partial "inline-partial" . }}
...
{{ partial "inline-partial" . }} {{/* Ignoring return values */}}
...
{{ define "inline-partial" }}
...
{{return $returnValue}}

{{end}}
```
{{< /hint >}}