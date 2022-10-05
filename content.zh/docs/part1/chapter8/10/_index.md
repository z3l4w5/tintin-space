---
weight: 10
title: "8.10 跨主题和网站的共享依赖项"
date: 2022-09-12T18:26:30+08:00
draft: true
---

# 8.10 跨主题和网站的共享依赖关系

我们将部分代码和短码从AcmeTheme模块复制到Acme Corporation网站，以便可以跨主题移植。 这导致内容重复，这使得维护变得困难。 我们可以潜在地从主题中删除短码，但主题和网站的功能都需要部分代码。 他们需要生活在主题中，这样它就可以在网站和网站中重复使用，这样我们就可以切换主题。 这种依赖关系是转移到单独模块的完美用例。

We can create a new module called AcmeCommon and move shared resources needed by both the Acme Corporation website and AcmeTheme. We set up the data in  the  folder  github.com/hugoinaction/AcmeCommon  (https://github.com/hugoinaction/hugoinaction/tree/chapter-08-resources/05).  Using  this  shared  repository in the theme and the website is an exercise for the reader. The reader should remove the shared layouts present in this repository from both repositories. You can browse the code at the code checkpoint ch08-8 to see this in action.

{{< hint info >}}
**Versions and shared dependencies**

If a Hugo-based website finds a dependency in two places, Hugo integrates only one version of the dependency even if different minor versions are present in various sources. Bundling multiple versions of a dependency is wasteful, increases bloat, and can make Hugo’s caching and, thereby, its performance suffer. Hugo expects its module developers to follow the Semver guidelines (https://semver.org/) and to introduce only breaking changes in a new major build.

Hugo can use multiple versions of a dependency (for example, 1.0 and 2.0 are major version changes, and 1.2 and 1.3 are not). It is strongly advised to remove this duplication to improve performance, disk utilization, and safety. This prevents unknown vulnerabilities from using unsupported older versions of dependencies.
{{< /hint >}}

{{< hint info >}}
**CODE CHECKPOINT**    https://chapter-08-08.hugoinaction.com, and source code: https://github.com/hugoinaction/hugoinaction/tree/chapter-08-08.
{{< /hint >}}

{{< hint warning >}}
**NOTE** 即使配置中存在，Hugo也不会将AcmeCommon模块添加到Acme Corporation网站的go.mo d文件中。 因为只能有一个AcmeCommon，所以没有必要添加两次。 当我们切换到不同的主题时，雨果会自动将AcmeCommon添加到go.mo d。
{{< /hint >}}