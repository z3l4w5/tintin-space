---
weight: 4
title: "8.4 Enabling themes other than Eclectic"
date: 2022-09-12T18:26:30+08:00
draft: true
---

# 8.4 Enabling themes other than Eclectic

Adding a theme to a Hugo website is as simple as replacing the URL in config.yaml,  but this may not always work. Theme switching can fail for a couple of reasons:

- Some themes require unique settings in the configuration to be usable.
- The website may be dependent on shortcodes that are not available in a differ- ent theme. Hugo will fail to compile in case of a missing shortcode.

Whereas a theme causes the first reason, the content creators can unknowingly cause the second. When we moved the layouts folder to AcmeTheme, we also moved the shortcodes that our website depends on. Although those shortcodes were available in Eclectic, they are not present in other themes like Universal. Therefore, if you take the source code at checkpoint 08-1 and try to replace the theme with any other that you find in the Hugo themes showcase, it will fail to build.

To keep the content independent of the theme, we need to have a copy of all the shortcodes used in the website, bundled in its codebase or loaded module (we will do this in section 8.10). To allow other themes, we will keep a copy of the partial and the shortcode folders in the core website. Copy the two folders from the themes/AcmeT- heme/layouts folder to the top-level layouts folder. Then you can use a different theme (like Universal) with the website by providing the GitHub path of the theme (for example, github .com/hugoinaction/Universal) in the theme section of the con- figuration. Note that because we got rid of the home page and have not configured the home page in Universal, the home page will be mostly blank at this point.

{{< hint info >}}
**CODE CHECKPOINT**    https://chapter-08-02.hugoinaction.com, and source code: https://github.com/hugoinaction/hugoinaction/tree/chapter-08-02.
{{< /hint >}}