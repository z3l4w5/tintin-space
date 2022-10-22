---
weight: 3
title: "7.3 提供taxonomy页面"
date: 2022-09-12T18:26:30+08:00
draft: true
---

# 7.3 提供taxonomy页面

有两种类型的分类页面：分类页面(用于每个分类术语)和术语页面(用于分类列表)。 术语页面提供了分类法中所有术语的列表 (例如，/tags处的所有标签)，而分类法页面列出了具有特定术语的所有页面 (如所有带有标签正方形的帖子)。 在覆盖任何页面之前，让我们看看它们在现有列表模板中的外观。 让我们用modern替换content/categories/_index中的类型作为级联属性，并查看页面的外观。 类别中的术语变成了类别的子页面，而各个帖子变成了每个分类页面的子页面。

Hugo试图通过将各种内容纳入两种类型的页面 (列表页面和单页) 来缓解主题作者的生活。 如果不存在相应的页面(单个模板用于单个页面)，则索引页、术语页和分类页面将退回到列表页。 我们可以通过分别为分类法页面和术语列表创建taxonomy.html和terms.html布局来覆盖这些页面。 因为列表模板不读取分类术语，所以像/Categories这样的位置还不会显示任何内容。

{{< hint warning >}}
**NOTE** 一个Hugo网站只需要两个模板: 一个list.html和一个single.html就可以完成。 请记住，在第4章中，Hugo中有两种捆绑包：分支捆绑包和页面捆绑包。 list.html和single.html这两个模板分别对应于这些bundle类型。 所有其它模板都是List模板的特例。 如果我们删除index.html，Hugo会为网站的索引页面选择list.html。 类似地，除非我们提供定制模板，否则分类页面使用列表模板来呈现。
{{< /hint >}}

{{< hint info >}}
**CODE CHECKPOINT**    https://chapter-07-08.hugoinaction.com, and source code: https://github.com/hugoinaction/hugoinaction/tree/chapter-07-08.
{{< /hint >}}

## 7.3.1 项目页面

term页面显示taxonomy中的term列表。 我们可以为各个term定义页面，并提供与其相关联的内容以提供摘要。 我们需要这样的东西是相当罕见的。 我们很少为我们在网站上使用的每个标签写摘要。 更好的演示是提供标签列表 (图7.7)。

{{< figure src="Figure7.7.svg" title="图7.7 Acme Corporation网站中类别taxonomy的term页面。 如果列表模板似乎不最适合特定页面，term页面将提供唯一变量来访问所有term并使用term中的页面。" >}}

在Layout/(https://github.com/hugoinaction/hugoinaction/tree/chapter-07-resources/06)./Terms.html中，我们将提供与我们将移动到部分(https://github.com/hugoinaction/hugoinaction/tree/chapter-07-resources/06)的子部分相同的最小细节。 请注意，由于并非所有分类法都有一个文件，因此我们需要将h3包装在部分检查中。 .Data.Terms变量允许访问给定分类类型中的所有术语。 我们有很多选择来获取此数据的排序版本。 按字母顺序，我们将在下面的列表中使用的是最受欢迎的。

{{< details title="Listing 7.17  Rendering a list of taxonomy terms (layout/modern/terms.html)" open=true >}}
![Listing7.17](Listing7.17.svg)
{{< /details >}}

请注意，在上一个列表中，term页面的标题来自网站配置 (例如，类别) 但可以通过为分类列表创建一个单独的_index.md来覆盖 (例如，content/categories/_index.md)。 下一个清单提供了subsection，用于将子部分呈现为卡片。 分类列表中的各个术语被呈现为一个小节。

{{< details title="Listing 7.18  Partial to render an individual term as a card in the taxonomy list" open=true >}}
```html
<li class="subsection">
<a href="{{.Permalink}}">
{{if .Title}}
<h3> {{.Title | humanize}} </h3>
{{else if .File}}
<h3>{{.File.Path | path.Dir | path.Base | humanize}}</h3>
{{end}}
<p>Pages: {{len .Pages}}</p>
{{$words:= 0}}
{{range .Pages}}
{{$words = add $words .WordCount}}
{{end}}
<p>Words: {{$words}}</p>
</a>
</li>
```
{{< /details >}}

{{< hint info >}}
**CODE CHECKPOINT**    https://chapter-07-09.hugoinaction.com, and source code: https://github.com/hugoinaction/hugoinaction/tree/chapter-07-09.
{{< /hint >}}

## 7.3.2 分类页面

大多数开发人员不需要覆盖分类法页面，因为列表模板对这些页面效果很好。 列表页面非常好，定制分类页面的一个很好的开始就是获取列表模板并创建一个名为axonomy.html的副本。 现在我们可以自定义taxonomy.html模板。 与分类页面相关联的部分是Terms页面，并且可以访问与Terms.html相关联的所有变量。 我们可以使用它来更改分类页面的标题，如下面的列表所示。

{{< details title="Listing 7.19 Changing the taxonomy title (layouts/modern/taxonomy.html)" open=true >}}
```html
<h1>
{{$.CurrentSection.Data.Singular | humanize}}
- {{.Title | humanize}}
</h1>
```
{{< /details >}}

{{< hint info >}}
**CODE CHECKPOINT**    https://chapter-07-10.hugoinaction.com, and source code: https://github.com/hugoinaction/hugoinaction/tree/chapter-07-10.
{{< /hint >}}

{{< hint warning >}}
**NOTE** Remember, in chapter 4, we provided both the singular and plural text  for a taxonomy. Hugo allows access to both the strings for our use. It does not automatically convert those because that cannot be reliably done across languages (not programming but human languages) without a vast database. We can use any of the strings as we see fit in the template.
{{< /hint >}}

{{< hint info >}}
**Exercise 7.4**

在Hugo的模板系统中，可以有意义地映射到所有其它模板的两个最重要的模板包括(选择两个)：
- a. list.html
- b. baseof.html
- c. terms.html
- d. taxonomy.html
- e. single.html
- f. index.html
- g. hugo.html
- h. partial.html
{{< /hint >}}