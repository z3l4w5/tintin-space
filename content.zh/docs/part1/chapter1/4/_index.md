---
weight: 4
title: "1.4 为什么使用Jamstack?"
draft: true
---

# 1.4 为什么使用Jamstack？

预先构建呈现给用户的HTML内容具有独特的优势 - 最少的操作；出色的性能；较低的成本。 我们将在以下各节中了解这些优点以及更多其它优点。

## 1.4.1 最少的操作

由于内容是在发布之前预先构建的，因此减少了站点中活动部件的数量。 服务提供商负责安全更新、硬件故障和网络问题。 云主机提供几乎100% 的正常运行时间，而无需网站所有者的任何积极参与。 无需随叫随到，无需考虑服务器、扩展、负载平衡、跨洲正常运行时间或任何其它运营开销。 开发人员可以专注于系统构建的乐趣，而企业可以专注于其核心能力，而不是建立一个DevOps团队。

## 1.4.2 出色的性能

CDN完全托管作为静态网站提供的预构建HTML。 这样，每个文件都被缓存，并从地理上靠近最终用户的服务器提供服务。  没有到应用程序服务器的往返，也没有数据库查询（这可能会成为瓶颈）。 大多数针对Jamstack的站点生成器在编译时生成HTML。 它已经完全可以在用户请求时直接呈现。 即使只有一个HTTP请求，该网站也可以正常运行。 使用Jamstack构建的简单网站可以在大多数审核中提供90% + 的性能评分。 如果开发人员在构建主题时对性能很敏感，那么基于Jamstack的网站可以在这些审计中达到100%的所有分数标准。

## 1.4.3 较低的成本

从托管栈中移除数据库和应用程序服务器可降低硬件成本。 随着操作变得自动，大多数DevOps需求都不存在。 所有这些都转化为显著的成本节约。 你可以使用静态网站主机 (如GitHub Pages和Netlify) 免费获得一个网站。 所有主要的云提供商，如AWS S3、谷歌云存储和Azure存储都提供低成本的静态托管。 无需拥有IT或DevOps团队来管理服务器团队。

## 1.4.4 开发人员生产力

像Git这样的版本控制系统管理基于Jamstack的网站。 没有必要拥有复杂的开发环境。 在开发人员机器上运行代码只有一个命令。 大多数网站可以通过简单的推送到服务器上一天多次部署。 这些功能使开发人员有时间和灵活性专注于网站的内容。

## 1.4.5 长寿

HTML/CSS是构建的最稳定技术。 今天的浏览器竭尽全力继续支持自20世纪90年代以来一直支持的所有功能。 如果你拥有一个基于Jamstack的网站，并且在互联网上消失了十年，当你回到你离开它的那个状态 (大部分) 时，它仍然会在那里。 除了静态服务器上托管的纯HTML、CSS或JavaScript之外，互联网无法保证对任何技术栈的支持。 你甚至可以在虚拟机中继续使用静态站点生成器，而无需更新版本。 因为生成器是本地的，所以生成器中的安全漏洞不会影响网站。 你不需要上网并将这些漏洞暴露给互联网。

## 1.4.6 工具

由于活动部件较少，结构定义明确，Jamstack的工具比其它web技术栈更先进，功能更强大。 通过Netlify、GitHub页面等直接支持扩展，即可实现一键部署。 将整个网站作为代码存在也意味着没有什么可隐藏的。 没有针对安全性或性能的复杂配置，没有针对技术栈中不同层的额外管理开销，也没有IDE (集成开发环境)。

{{< hint info >}}
**在运行中更新**

对于Jamstack来说，这似乎是一个限制，我们不能动态更新网站。 大多数传统系统都提供管理员模式来更新网站。 Jamstack没有开出任何药方。 使用Jamstack，不需要任何特殊工具来更新基于Jamstack的网站。

标记语言友好且易于使用。 我们可以在任何文本编辑器中提供更新。 大多数版本控制提供商，如GitHub、GitLab和BitBucket，都可以从浏览器提交新的更改。 持续集成可以自动构建并将其部署到生产中。 我们获得了对我们的内容拥有完整版本控制系统的好处。 我们也可以自由选择我们的文本编辑器。 作为额外的奖励，我们可以随时随地更新主题。 文本内容，自动部署和持续集成确保我们不会错过WordPress的管理模式，但是如果需要，也可以使用专有管理工具。 我们将在附录C中讨论Netlify CMS。
{{< /hint >}}