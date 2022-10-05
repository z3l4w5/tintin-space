---
weight: 10
title: "1.10 Hugo不适合的场景"
date: 2022-09-12T18:26:30+08:00
draft: true
bookToc: false
---

# 1.10 Hugo不适合的场景

像所有工具一样，Hugo也有自己的使用场景。 除了由于Jamstack框架的固有Jamstack限制之外，我们需要了解Hugo的重点仅在于Jamstack的标记部分。 虽然Hugo提供了最快的JavaScript bundler，并对NPM生态系统有很好的支持，但它对Jamstack的JavaScript和API层采取了一种不插手的方式。 如果你想构建一个需要大量JavaScript与静态页面混合的工具，或者你想拥有一个与网站模板共享代码的应用编程接口，仅Hugo独立于这些部分的开发方式是不够的。

当我们需要一些Hugo没有的功能时，Hugo可能不是最优的，而我们无法通过API实现这一点。 Hugo保持模板和模块无法访问其核心，以保持其灵活性并保持其性能不变。 对于想要定制一个静态站点构建器的开发人员来说，Hugo可能不是正确的选择，因为那需要很多插件来迎合不常见的场景。 例如，如果我们需要在编译时与SOAP或FTP协议进行交互，则Hugo可能无法做到这一点 (到v0.91.2版为止)。