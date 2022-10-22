---
weight: 4
title: "7.4 Creating our own theme"
date: 2022-09-12T18:26:30+08:00
draft: true
---

# 7.4 Creating our own theme

Now that we have moved the significant parts of our theme onto the modern layout,    we don’t need Eclectic anymore. We can safely remove it from our codebase and move all the pages over to our custom theme.

## 7.4.1 Moving to a new theme
To move to a custom theme, we need to make sure we do not use any feature from Eclectic. We don’t want broken pages that need more work in our new theme. Note that we do not need to replicate all Eclectic features. Just focus on what we need and then decide about content that we can remove. For verification, we will add a cascading type switch on the index page of the website to the content type modern as the following listing demonstrates.

{{< details title="Listing 7.20  Moving all pages to content type modern (content/_index.md)" open=true >}}
```yaml
cascade:  
  type: modern
```    
{{< /details >}}

{{< hint warning >}}
**NOTE** We can use the Hugo configuration to provide the top-level cascade property as well. This lets us keep this configuration outside of content.
With this change, we have applied content type modern to all pages on the website. We can verify that the website looks good without the theme. Note that there are broken pages like data-driven.md because we did not add support for using its front matter keys to create some elements. We do not need this page in the Acme Corporation website, so we can remove the themes/eclectic folder and the theme: eclectic setting from config/_default/config.yaml.
{{< /hint >}}

{{< hint info >}}
**CODE CHECKPOINT**    https://chapter-07-11.hugoinaction.com, and source code: https://github.com/hugoinaction/hugoinaction/tree/chapter-07-11.
{{< /hint >}}

The next step is moving the layout to a different theme. The concept of a theme in Hugo is fluid. Websites can pick and choose parts of their template content and move that to a theme. To create a new theme, we need to create a subfolder in the themes folder with the theme’s name. We can choose to name the theme whatever we want. For this book, we chose AcmeTheme as the theme name. We can move the layouts folder to the themes/AcmeTheme folder to promote the layouts as part of the theme. Next, we need to update the theme in the configuration file, config/_default/config.yaml. The following listing updates the theme.

{{< details title="Listing 7.21  Setting the theme to AcmeTheme (config/_default/config.yaml)" open=true >}}
```yaml
theme: AcmeTheme
```
{{< /details >}}  	

{{< hint info >}}
**CODE CHECKPOINT**    https://chapter-07-12.hugoinaction.com, and source code: https://github.com/hugoinaction/hugoinaction/tree/chapter-07-12.
{{< /hint >}}

We should get the same website with all pages built using our modern type if we run the code in listing 7.21. We can then get rid of the Eclectic theme completely by deleting it from the themes folder.

## 7.4.2 Aligning content with the theme

Technically, we now have a theme. A significant conceptual difference between a content type (or any other parts of a theme that we have overridden so far) and the theme is that we build a theme for reuse across multiple websites. But now, it is tightly coupled with the content structure. If we had picked up the project after chapter 4 (using code checkpoint chapter-04-11) and had swapped its theme with the one we have right now, nothing would work. We need to provide meaningful defaults and make it easy for someone to pick up the theme with a barebones Hugo project. All added functionality can be made accessible via the configuration, front matter, or hardcoded file locations (like we have for background.svg), but the base functionality should be readily available.

The first step is to remove the requirement of the content type. To do this, we need to  rename  themes/AcmeTheme/layouts/modern  to  themes/AcmeTheme/layouts/_default, which makes our layout the default layout. The code we have should continue to work even though it references the content type modern. In the absence of a content type, Hugo falls back to the default content type. We can now remove type: modern from our codebase completely.

{{< hint info >}}
**CODE CHECKPOINT**    https://chapter-07-13.hugoinaction.com, and source code: https://github.com/hugoinaction/hugoinaction/tree/chapter-07-13.
{{< /hint >}}

We moved the Blog pages to a new layout called blog. There is a discoverability problem with layouts in Hugo. Unless someone knows about it, the likelihood of not finding a layout is high. It makes much more sense for the blog to be a new content type. Therefore, we will create a new folder called themes/AcmeTheme/layouts/blog and move   themes/AcmeTheme/layouts/_default/blog.html   to   themes/AcmeTheme/ layouts/blog/single.html. This way, all the pages in the blog folder are automatically selected with the content type blog and use the single.html template.

It is great to see the Blog pages picking up this information automatically. If a particular layout is absent, Hugo falls back to the default layout for that file. Because the single layout exists in the blog folder, the entries in that folder automatically pick this up. With this, we can remove the layout changes in the front matter of the Blog pages.

{{< hint info >}}
**CODE CHECKPOINT**    https://chapter-07-14.hugoinaction.com, and source code: https://github.com/hugoinaction/hugoinaction/tree/chapter-07-14.
{{< /hint >}}

When we created the blog content type, the blog’s single.html template automatically picked up the base template (baseof.html) from the _default type. Even the base templates can fall back to the default type if they are not present in a specific content type. The default content type is unique in Hugo because it can provide the base template to all content types. Therefore, most default base templates are generic and extensible. That we need entirely independent HTML pages on the same website is
sporadic. If we override the default content type in a theme, it is challenging for the rest of the theme to function correctly.

## 7.4.3 Providing theme assets

The templates defined in the theme refer to multiple assets like CSS files and images in the assets folder. We need to move these to the themes/AcmeTheme folder to make the theme independent. Although moving the CSS files is not a big issue, the logo and the products.csv file information is specific to the Acme Corporation website and does not belong to the theme. We can place the empty products.csv and the placeholder images in  the  theme  folder  to  allow  the  website  to  compile  and  execute  (https://github
.com/hugoinaction/hugoinaction/tree/chapter-07-resources/07). Once we move the CSS file and provide the theme assets, the theme should potentially stand on its own.

{{< hint info >}}
**CODE CHECKPOINT**    https://chapter-07-15.hugoinaction.com, and source code: https://github.com/hugoinaction/hugoinaction/tree/chapter-07-15.
{{< /hint >}}

{{< hint warning >}}
**NOTE** You will need to change the theme name to Acme in the configuration to pick up this theme.
{{< /hint >}}

To check this, we can move the source code (content and config folders) from chapter 4, empty the assets and archetypes folders, and then test.

{{< hint info >}}
**CODE CHECKPOINT**	https://chapter-07-16.hugoinaction.com, and source code: https://github.com/hugoinaction/hugoinaction/tree/chapter-07-16. (reverted in chapter-07-17)
{{< /hint >}}

The theme we have just created is ready to be used outside of our website. We can now host it independently in its own separate repository or provide it as a folder to be integrated by other websites. We can also submit this theme to the Hugo theme gallery.

{{< hint warning >}}
**NOTE** Not all Hugo websites create independent themes. If you are building a theme just for your website, keeping it in this state in the themes folder may be the best approach.
{{< /hint >}}

Having a theme embedded in the website provides maximum ease of use as you only have to manage one code repository; you only need to cater to the content of a single website rather than a general-purpose use case for multiple. You then get all the flexibility of a theme without the overhead of multiple repositories for your code.

All themes do not need to be shared publicly. You can have multiple websites with the same shared theme used within an organization. The sales team can have their independent website with a content folder, while the documentation team can set up a separate website as well. They all can share a custom theme managed by the engineering team.

{{< figure src="Figure7.8.svg" title="Figure 7.8 Remove the data: reusable themes make some jobs like sharing only a piece of the website simple. Alex persuades the marketing team to try this lightweight approach." >}}