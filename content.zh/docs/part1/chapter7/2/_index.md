---
weight: 2
title: "7.2 通过提供内容和小节列表来更新索引页面"
date: 2022-09-12T18:26:30+08:00
draft: true
---

# 7.2 通过提供内容和子列表更新索引页

The index pages like /blog need to have a different interface than the regular pages. Rendering it with the blog layout renders only the Markdown content, and we lose the capability to navigate to the child pages in the section and the subsections. These pages deserve separate templates.

## 7.2.1 使用索引页面的列表模板

The index pages provide access to the content within a section. Because we have multiple content pages, the index pages have a list of pages. These are called list pages. Hugo allows list pages to have a different template to render content differently.

Let’s create a file called list.html in the modern subfolder in the layouts directory.  In the index page, we need to provide a list of pages in the section. If a page has child pages, those are available in the .RegularPages variable for the page. We can loop through  these  pages  to  provide  a  list  of  child  pages  for  navigation  (https://github.com/hugoinaction/hugoinaction/tree/chapter-07-resources/03). The following listing shows how to provide the list of pages for the Acme Corporation website.

{{< details title="Listing 7.9  Getting a list of pages (layouts/modern/list.html)" open=true >}}
![Listing7.9](Listing7.9.svg)
{{< /details >}}    

In blog/_index.md, we can return the modern content type for all the pages where the kind is section. The following listing sets up these pages as the list type for the Blog pages. The blog index page will then render with the list of pages directly in that section with these changes.

{{< details title="Listing 7.10  Setting the kind section as the list type (content/blog/_index.md)" open=true >}}
```markdown
---
cascade:
    - _target:
        kind: section 
        type: modern 
        layout: list
---
```
{{< /details >}}

{{< hint info >}}
**CODE CHECKPOINT**    https://chapter-07-04.hugoinaction.com, and source code: https://github.com/hugoinaction/hugoinaction/tree/chapter-07-04.
{{< /hint >}}

## 7.2.2 创建多个页面以呈现长列表

We loop through all the pages in a section to form the index page. One problem with this approach is that all pages will render together on a single page even if we have hundreds of posts. That would turn this into a heavy web page and cause a slow down when loading. But if we restrict to a smaller number of posts (like we did on the index page using the first function), all the posts will not be navigable. We need a mechanism to provide multiple pages with all the posts generated from one template (figure 7.5). Hugo answers this problem with the Paginator object.

{{< figure src="Figure7.5.svg" title="图7.5启用了分页的博客项目的列表页面。 (Images by Michael Schwarzenberger, gefrorene_wand, and Robert Wilkos on Pixabay.)" >}}

Paginator is a Hugo object used to create multiple pages from a single function call. We can use .Paginator.Pages in the loop instead of .RegularPages as in the following listing and set the pagination options in the website configuration file. The .Paginator object automatically splits the list of pages into multiple pages and supplies the right set of pages to render.

{{< details title="Listing 7.11 Splitting the index page (layouts/modern/list.html)" open=true >}}
```html
{{ with .Paginator.Pages }}
<ul class="posts">
```
{{< /details >}}

Because we have a small number of posts, we need to change the number of posts per index page to trigger pagination. The following listing changes the number of elements in a page in config.yaml for the paginator to take effect.

{{< details title="Listing 7.12 Updating the pagination options (config/_default/config.yaml)" open=true >}}
![Listing7.12](Listing7.12.svg)
{{< /details >}}    

{{< hint info >}}
**Grouping pages**

Hugo supports grouping pages into arbitrary groups using the .Pages.GroupBy set of methods. For example, if we want to show pages with headings based on the creation year, we could use the {{range .Pages.GroupByDate "2006"}} and then set the year as the .Key and .Pages as all pages with that key. This sample code is not added to the chapter resources, but you can add it to layouts/modern/list.html.

```html
{{ range .Pages.GroupByDate "2006" }} Posts in year {{ .Key }}:
{{range .Pages}}
<a href="{{.Permalink}}"> {{.Title}}</a>
{{end}}
{{end}}
```
{{< /hint >}}

代码段按年份对所有页面进行分组。 然后循环遍历各个年份，在.Key字段中为它们提供属于.Pages字段中的年份的页面。 我们也可以将Paginator对象用于页面组。

要启用页码，我们可以使用.Paginator对象中的属性 (例如，TotalPages，Next，First，PageNumber等)。 Hugo附带了一个内部模板，我们也可以将其用于此任务。 以下列表启用了内部模板，该模板大部分是完整的，很少被主题覆盖。

{{< details title="Listing 7.13  Using the pagination template (layouts/modern/list.html)" open=true >}}
```html
{{ template "_internal/pagination.html" . }}
```
{{< /details >}}

虽然默认的分页模板很好，但简洁的分页模板(清单7.14)构建得更快，因此建议使用它。 该模板的副本存在于资源章节中，以防万一它在Hugo的未来版本中被修改 (https://github.com/hugoinaction/hugoinaction/tree/chapter-07-resources/04).

{{< details title="Listing 7.14 Using the terse format (layouts/modern/list.html)" open=true >}}
```html
{{ template "_internal/pagination.html" (dict "page" . "format" "terse") }}
```
{{< /details >}}

现在，我们可以更新新闻索引页以使用现代内容类型。 分页不会显示在新闻部分，因为它只有一页。

{{< hint info >}}
**CODE CHECKPOINT**    https://chapter-07-05.hugoinaction.com, and source code: https://github.com/hugoinaction/hugoinaction/tree/chapter-07-05.
{{< /hint >}}

{{< hint info >}}
**Exercise 7.3**

是什么让我们可以在Hugo中将单个数组拆分到多个页面？
- a. List template
- b. Bundle
- c. Cascade
- d. Content type
- e. Paginator
- f. Taxonomy
{{< /hint >}}

## 7.2.3 使用自定义分页程序

内置的.Paginator有一组很好的缺省值，在大多数情况下，对于索引页来说就足够了。 如果需要，我们可以进一步定制该页面。 隐藏在Acme Corporation网站上的一个部分中的社区博客帖子不会获得太多点击量。 因此，管理层希望将它们添加到常规博客列表中。 默认分页不包括所有子页面，而只包括直接子页面。 我们需要使用自定义分页程序来同时使用节和小节页面，如下面的清单所示。 为此，.Pagate函数获取页面列表。

{{< details title="Listing 7.15 Adding a custom paginator (layouts/modern/list.html)" open=true >}}
![Listing7.15](Listing7.15.svg)
{{< /details >}}    

此代码从一级更深层次的小节中读取页面，并将其附加到 $pages变量中。 如果我们需要导航整个树，我们需要编写一个递归部分模板。 当我们创建自定义分页器时，Hugo不会生成默认分页器。

{{< hint warning >}}
**NOTE** 我们可以使用Pagate属性将配置中指定的页面大小作为附加参数传递给.Pagina函数，从而覆盖该页面大小。 例如。分页 $ 帖子5将5个帖子放在一页中。
{{< /hint >}}

## 7.2.4 呈现子部分列表

社区博客是网站博客部分的一个小节。 每个索引页都有一个名为.Sections的变量，它获取索引页的子节的列表。 使用此变量使我们可以显示具有当前页面的每个部分的子页面。 如果不在列表页面上提供子部分的列表，我们就会留下无法访问的页面。 在本节中，我们还将在第一部分页面中添加子节列表 (图7.6)。

{{< figure src="Figure7.6.svg" title="图7.6使用列表而不是索引模板的Acme Corporation网站的索引页。 (Images by tookapic, ds_30, and Robert Wilkos on Pixabay.)" >}}

我们可以使用Paginator对象来检测这是否是第一页 (https://github.com/hugoinaction/hugoinaction/tree/chapter-07-resources/05).  如果用户在第1页，我们可以显示帖子的标题(对应子部分)和子部分的列表。 以下列表使用:节的索引页中的节，以提供Hugo模板中的小节。

{{< details title="Listing 7.16  Providing the list of subsections (layouts/modern/list.html)" open=true >}}
![Listing7.16](Listing7.16.svg)
{{< /details >}}    

{{< hint info >}}
**CODE CHECKPOINT**    https://chapter-07-06.hugoinaction.com, and source code: https://github.com/hugoinaction/hugoinaction/tree/chapter-07-06.
{{< /hint >}}

这里需要注意的是，如果我们有多个子部分，就不能有多个分页器 (一个用于页面，另一个用于小节)。 一个页面只能有一个分页器。 存在此限制是因为如果我们每页有两个分页 (例如，子部分和帖子)，我们将需要支持独立导航 (例如，张贴第2页带有小节第1页、张贴第3页带有小节第1页、张贴第2页带有小节2、张贴第3页带有第2小节，依此类推)。 双分页有指数 (O(nk)) 组合 (到n个分页和各k个页面)，这是缓慢和浪费的。

{{< hint info >}}
**CODE CHECKPOINT**    https://chapter-07-07.hugoinaction.com, and source code: https://github.com/hugoinaction/hugoinaction/tree/chapter-07-07.
{{< /hint >}}