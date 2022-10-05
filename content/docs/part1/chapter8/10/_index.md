---
weight: 10
title: "8.10 Shared dependencies across the theme and website"
date: 2022-09-12T18:26:30+08:00
draft: true
---

# 8.10 Shared dependencies across the theme and website

We copied over the partial and shortcodes into the Acme Corporation website from the AcmeTheme module to be portable across themes. That led to duplication of con- tent, which makes it difficult to maintain. We can potentially remove the shortcodes from the theme, but the partials are needed for both the theme and for the website to function. They need to live in the theme, so that it is reusable across websites, and in the website, so we can switch themes. This dependency is the perfect use case for mov- ing to a separate module.

We can create a new module called AcmeCommon and move shared resources needed by both the Acme Corporation website and AcmeTheme. We set up the data in  the  folder  github.com/hugoinaction/AcmeCommon  (https://github.com/hugo- inaction/hugoinaction/tree/chapter-08-resources/05).  Using  this  shared  repository
in the theme and the website is an exercise for the reader. The reader should remove the shared layouts present in this repository from both repositories. You can browse the code at the code checkpoint ch08-8 to see this in action.

{{< hint info >}}
**Versions and shared dependencies**

If a Hugo-based website finds a dependency in two places, Hugo integrates only one version of the dependency even if different minor versions are present in various sources. Bundling multiple versions of a dependency is wasteful, increases bloat, and can make Hugo’s caching and, thereby, its performance suffer. Hugo expects its module developers to follow the Semver guidelines (https://semver.org/) and to intro- duce only breaking changes in a new major build.

Hugo can use multiple versions of a dependency (for example, 1.0 and 2.0 are major version changes, and 1.2 and 1.3 are not). It is strongly advised to remove this dupli- cation to improve performance, disk utilization, and safety. This prevents unknown vul- nerabilities from using unsupported older versions of dependencies.
{{< /hint >}}

{{< hint info >}}
**CODE CHECKPOINT**    https://chapter-08-08.hugoinaction.com, and source code: https://github.com/hugoinaction/hugoinaction/tree/chapter-08-08.
{{< /hint >}}

{{< hint warning >}}
**NOTE** Hugo does not add the AcmeCommon module to the go.mod file of the Acme Corporation website even though it is present in the configuration. Because there can be only one AcmeCommon, there was no point in adding it twice. Hugo adds AcmeCommon to go.mod automatically when we switch to a different theme.
{{< /hint >}}