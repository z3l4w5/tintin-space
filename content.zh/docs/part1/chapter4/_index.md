---
weight: 4
bookFlatSection: true
title: "第4章 使用Hugo进行内容管理"
bookToc: false
bookCollapseSection: true
---

# 第4章 使用Hugo进行内容管理

{{< hint info >}}
**本章涵盖**
- 在Hugo网站中将页面组织成sections和menus
- 使用Hugo taxonomies对相关内容进行分组
- 将页面内容捆绑到页面bundle中
- 使用Hugo的内置和社区提供的shortcodes来实现更多的Markdown功能
{{< /hint >}}

网站不仅仅是散布在随机URL位置的一堆网页。 这些页面需要是可发现的，需要组织成有意义的部分，需要有一种方法导航到它们，读者才能成功访问。 大多数网站的内容都有布置策略。页面中包含分组，标记和导航提示，供读者导航到其它页面。

网站的开发团队有两个截然不同的角色：内容所有者和主题开发人员。 内容所有者决定网站上显示的内容，而主题开发人员则专注于显示内容。 在本章中，我们将扮演Acme Corporation网站的内容所有者(也称为网站作者或网站编辑)角色。

我们将在本章中研究内容组织和管理 (见图4.1)。 在第4.1节中，我们将在配置文件夹中组织配置。 在4.2至4.4节中，我们将讨论在Hugo网站上管理和关联内容的方法。 第4.5节将介绍shortcodes，这些shortcodes位于layout文件夹中。 Shortcodes提供了在Hugo不同页面之间扩展Markdown和共享内容的方法。

![Figure4.1](Figure4.1.svg)

图4.1 网站编辑和开发人员将网站的内容组织到文件和文件夹中，然后存储在content目录中。 本章主要介绍优化资源管理的content目录的组织。 我们还将在config文件夹中组织配置，并在layouts文件夹中创建shortcodes以扩展Markdown。
