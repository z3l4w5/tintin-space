---
weight: 11
title: "8.11 内容插件"
date: 2022-09-12T18:26:30+08:00
draft: true
---

# 8.11 内容插件

模板插件是模板代码的有用抽象，我们可以重复使用。 Hugo Modules还允许我们拥有内容插件，这些插件可以打包我们可以在多个网站上重复使用的内容。

可在众多网站上共享的内容的一个例子是使用条款和隐私政策页面。 同一公司的网站共享相同的使用条款页面。 我们可以将此页面移动到一个独立的模块，并将其导入所有公司网站以供重复使用。 该页面可以使用内置的param函数从配置中访问站点参数，还可以捆绑ShortCode以跨多个网站提供标准化数据。

我们需要在Acme保护伞下的所有网站上使用相同的使用条款和隐私政策页面。 Acme Corporation网站的使用条款和隐私政策页面也存在于存储库i n github.com/hugoinaction/ TermsAndPrivacy (https://github.com/hugoinaction/hugoinaction/tree/第08章-资源/06) 中。 菜单项在前面，硬编码的数据值(在不同的网站上可能不同)被替换为参数短码(例如，公司名称的{{&lt；param“TermsAndPrival y.Company_name”&gt；})。 执行这些更改已成为读者的练习。

![Figure8.4](Figure8.4.svg)

图8.4个月的工作：Bob面临着愤怒的营销主管的首当其冲，因为他没有一个中央位置来保存使用条款和隐私政策页面，这使得旧的使用条款在法律上使营销活动处于风险之中。

我们将把一个插件集成到Acme Corporation网站 (而不是Acme Corporation主题) 中，并将其配置为摆脱我们的硬编码使用条款和隐私政策页面。 要将此插件集成到Acme Corporation网站，我们需要执行以下步骤。
- 1 删除terms.md和privacy.md页面。
- 2 使用以下清单 (https://github.com/hugoinaction/hugoinaction/tree/ chapter-08-resources/07) 中的内容更新config/_default文件夹中的module.yaml文件。

{{< details title="Listing 8.11 Adding a new dependency (config/_default/module.yaml)" open=true >}}
```yaml
imports:
  - path: github.com/hugoinaction/TermsAndPrivacy
...
```
{{< /details >}}

- 3 将术语和隐私参数添加到TermsAndPrivacy存储库的配置中，如清单所示。

{{< details title="Listing 8.12  Adding the parameters (config/_default/params.yaml)" open=true >}}
```yaml
TermsAndPrivacy:
  company_name: Acme Corporation 
  contact_email: contact@example.org 
  website: https://hugoinaction.com 
  contact_dpo_email: dpo@hugoinaction.com 
  contact_dpo_phone: 9999999999
```
{{< /details >}}

- 4 添加菜单文件以带回页脚菜单项，如下面的列表所示。

{{< details title="Listing 8.13 Restoring the footer entries (config/_default/menu.yaml)" open=true >}}
```yaml
footer:
    - name: Privacy Policy
      weight: 300
      url: /privacy
    - name: Terms of Use
      weight: 200
      url: /terms
```
{{< /details >}}

{{< hint info >}}
**CODE CHECKPOINT**    https://chapter-08-09.hugoinaction.com, and source code: https://github.com/hugoinaction/hugoinaction/tree/chapter-08-09.
{{< /hint >}}

隐私政策和使用条款页面从具有这些更改的共享内容模块加载。 此模块是通用的，你可以自由地将其用于Acme Corporation和Hugo in Action之外的自己的网站。

{{< hint info >}}
**Exercise 8.3**

关于内容插件，以下哪项陈述是正确的？(选择所有适用的选项。)
- a. A content plugin creates a link to the shared content in the generated website.
- b. A content plugin cannot have template code.
- c. A content plugin can be used to set up access control on the content by splitting each area into a separate repository.
- d. A content plugin moves the common content into a separate repository for one place of access.
{{< /hint >}}