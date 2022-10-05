---
weight: 5
title: "7.5 Powering up with content views"
date: 2022-09-12T18:26:30+08:00
draft: true
---

# 7.5 Powering up with content views

With a theme, we get access to multiple content types. We already saw how content types can automatically map to section names. A content type also can have content views. Content views are partial layouts rendered inline in another layout. Creating these is similar to creating a layout. To understand the problem content views solve, navigate to the public category page on the Acme Corporation website (http://localhost:1313/ categories/public/). It contains three pages: Circle, Curve, and Shaper. Although Circle and Curve come from the website’s blog section, the Shaper page comes from the news section. The news section looks different from the blog section of the website and has a separate template. But the taxonomy template is shared between these sections. Content views are subtemplates that we can render from inside another template. We need to move the card view, themes/AcmeTheme/layouts/partials/card.html, to the default entry for the card template, themes/AcmeTheme/layouts/_default/card.html. Listing 7.22 shows how we can call this template in all referring pages via the Page
.Render function. Note that in the following listing, you will need to make this change
to theme/AcmeTheme/layouts/_default/taxonomy.html, theme/AcmeTheme/layouts/
_default/list.html,  theme/AcmeTheme/layouts/blog/single.html,  and  theme/Acme Theme/layouts/_default/index.html.

{{< details title="Listing 7.22  Rendering the card view via a content view instead of a partial" open=true >}}
```
{{.Render "card"}}
```
{{< /details >}}

Now we can create card.html for the news section, which is different from a regular card and can uniquely identify that section (figure 7.9). Note that we will create a different content type for the News pages to map to the news section automatically.

{{< figure src="Figure7.9.svg" title="Figure 7.9 The public category page with a different card view for the news section, which contains a badge to highlight it. (Images by PublicDomainPictures, Free-Photos, and tookapic on Pixabay.)" >}}

We can decide not to override any other layouts and leave those to use the default layout (https://github.com/hugoinaction/hugoinaction/tree/chapter-07-resources/08).  The following listing adds a badge to news posts in the news specific card.html. With these changes, the news section should be easily identifiable everywhere as a card.

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

Which of the following are features of content views? (Select all that apply.)
- a. Content views are not cached and generated each time the view is used.
- b. Content views allow arbitrary arguments to be passed to the content.
- c. Content views are rendered in the same context as the parent layout.
- d. Content views can be rendered from within another layout.
- e. Content views can be overridden based on the content type.
- f. Content views can be overridden based on the layout.
{{< /hint >}}

Creating a theme is a significant accomplishment in a developer’s journey into Hugo. A theme author masters the Go template language and understands the critical prin- ciples of laying out content and the internal features that ensure outstanding perfor- mance in a Hugo-based website. Theme authors can map any content to a website and effectively use all the power and flexibility provided by Hugo.