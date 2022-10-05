---
weight: 5
title: "7.5 使用内容视图启动"
date: 2022-09-12T18:26:30+08:00
draft: true
---

# 7.5 为内容视图提供动力

通过主题，我们可以访问多种内容类型。 我们已经了解了内容类型如何自动映射到部分名称。 内容类型也可以具有内容视图。 内容视图是以内联方式在另一个布局中呈现的部分布局。 创建这些类似于创建布局。 要了解内容视图解决的问题，请导航到Acme Corporation网站上的公共类别页面(http://localhost:1313/Categories/PUBLIC/)。 它包含三页: 圆、曲线和整形器。 尽管Circle和Curve来自网站的博客部分，但Shaper页面来自新闻部分。 新闻版块看起来与网站的博客版块不同，并有单独的模板。 但是分类模板是在这些部分之间共享的。 内容视图是我们可以从另一个模板内部呈现的子模板。 我们需要将卡片视图Themes/AcmeTheme/Layout/Partials/card.html移到卡片模板的默认条目Themes/AcmeTheme/Layout/_Default/card.html。 清单7.22显示了如何通过Page.Render函数在所有引用页面中调用此模板。 注意，在下面的清单中，你将需要对theme/AcmeTheme/layouts/_default/taxonomy.html，theme/AcmeTheme/Layout/_Default/List.html、Theme/AcmeTheme/Layout/Blog/Single.html和Theme/Acme Theme/Layout/_Default/index.html进行此更改。

{{< details title="Listing 7.22  Rendering the card view via a content view instead of a partial" open=true >}}
```
{{.Render "card"}}
```
{{< /details >}}

现在，我们可以为新闻部分创建card.html，它不同于常规卡，并且可以唯一地标识该部分 (图7.9)。 请注意，我们将为News页面创建不同的内容类型，以自动映射到新闻部分。

{{< figure src="Figure7.9.svg" title="图7.9了 “公共类别” 页面，其中包含用于突出显示的徽章，其中包含 “新闻” 部分的其他卡片视图。 (Images by PublicDomainPictures, Free-Photos, and tookapic on Pixabay.)" >}}

我们可以决定不覆盖任何其他布局，而让这些布局使用默认布局(https://github.com/hugoinaction/hugoinaction/tree/chapter-07-resources/08).  下面的清单为新闻特定card.html中的新闻帖子添加了徽章。 有了这些变化，新闻版块在任何地方都应该很容易被识别为卡片。

{{< details title="Listing 7.23  Adding a badge to news posts" open=true >}}
```html
<li class="post news-item">	Adds the news-item class

<div class="badge"> News
</div>
...
</li>

Adds a badge for the
news summaries
```
{{< /details >}}

{{< hint info >}}
**CODE CHECKPOINT**    https://chapter-07-18.hugoinaction.com, and source code: https://github.com/hugoinaction/hugoinaction/tree/chapter-07-18.
{{< /hint >}}

{{< hint info >}}
**Exercise 7.5**

以下哪些是内容视图的特征？(选择所有适用的。)
- a. Content views are not cached and generated each time the view is used.
- b. Content views allow arbitrary arguments to be passed to the content.
- c. Content views are rendered in the same context as the parent layout.
- d. Content views can be rendered from within another layout.
- e. Content views can be overridden based on the content type.
- f. Content views can be overridden based on the layout.
{{< /hint >}}

创建主题是开发人员进入Hugo之旅中的一项重大成就。 主题作者掌握Go模板语言，并了解布局内容的关键原则以及确保在基于Hugo的网站中出色表现的内部功能。 主题作者可以将任何内容映射到网站，并有效地使用Hugo提供的所有功能和灵活性。