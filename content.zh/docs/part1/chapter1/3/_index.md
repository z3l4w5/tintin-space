---
weight: 3
title: "1.3 Jamstack中的JAM"
draft: true
---

# 1.3 Jamstack中的JAM

Jamstack的JAM部分代表JavaScript、APIs和Markup(标记)。 让我们逐个看看这些组件。

## 1.3.1 JavaScript

Jamstack中的JavaScript是指提供交互性和动态功能的所有客户端脚本编写方法，这些方法对用户是个性化的，不能预编译。 这使开发人员能够对用户操作做出反应，并在运行时修改用户界面。 Jamstack将JavaScript框架及其管理的细节留给了web开发人员。

在传统的技术栈中，服务器在处理用户交互方面扮演着突出的角色。 即使仅需要修改页面的一部分，它也会生成新页面。 这是不必要的，也不是最优的。 现代JavaScript完全能够将用户状态存储在浏览器中。 它可以与服务器通信并更新界面，而用户不需要重新加载或看到界面中的闪烁。 Jamstack规定使用JavaScript来处理的最佳场景是 - 向最终用户提供交互式界面，并进行从客户端到服务器进行通信。

## 1.3.2 应用程序编程接口 (APIs)

应用程序编程接口 (api) 为与web服务进行通信提供了定义明确的合同。 API抽象了整个服务器功能，因此客户端不需要了解服务器内部结构即可使用服务。 在Jamstack中，预编译和客户端JavaScript接管了通常在服务器上完成的许多工作， 但服务器仍有其使用场景。 这些包括跨机器存储应用程序状态，需要比单台机器更多处理能力的计算，以及必须从网站浏览者传输回服务器的数据。 许多传统系统公开api与底层功能进行通信。 虽然这种方法符合Jamstack的定义，但Jamstack建议尽量减少API的构建，以减少维护开销。 Jamstack与许多需要其它技术栈中API的操作处理方式不同。 针对内容的创建，更新或删除的API过程，你应该在磁盘上新建，更新或删除文件。 只有基于用户在网站上的操作(如购买和评论)的动态更新才需要专用API。

有第三方API提供程序提供高级API，开发人员可以使用这些API，而无需自己构建所有东西。 从处理注释到全文搜索，无需编写自定义代码即可大规模使用。 当我们需要编写自定义后端时，云服务提供商让这项任务比从头开始构建更容易。 借助FaaS，云服务提供商可以接管正常运行时间，持续的安全更新以及随用户负载扩展的所有权。 服务提供商在全球范围内维护性能和可用性。 开发人员编写代码并将其交给服务提供商进行部署。 需要持续进行的工作量微乎其微。 然后，开发人员可以努力增强功能或在功能级别上更新任何依赖项。

## 1.3.3 Markup

在文本文档中“标记”的传统定义指一组注解 (例如HTML文档中的XML标记或Markdown中的文本周围的星形加粗标记)，这些注解提供了有关如何理解或呈现文本的更多信息。 Jamstack将整个标记文档视为标记。 它由文本数据，注释和结构化元数据组成。

标记形成了Jamstack的数据层。 与传统数据库不同，我们将标记存储在文本文件中。 它的原始形式是可读和可编辑的，而无需使用工具将其转换为可读格式。 标记语言提供了一种以简洁可读的方式编写格式化文档的方法。 Markdown是在Jamstack中编写内容的最流行的标记语言。(我们将在第3章中详细研究Markdown。)我们用于与文档相关的其它信息的各种元数据语言可以随此内容一起使用。 其中之一是YAML (Yaml Ain’t Markup Language 缩写)，我们也将在第3章中讨论。

{{< hint warning >}}
**NOTE** 超文本标记语言(HyperText Markup Language)也是一种标记语言，你也可以自由选择它来将数据写入Jamstack。 但是，诸如Markdown之类的人类可读语言使阅读和维护我们的数据变得更加容易。 标记文件在渲染期间转换为HTML，而在内容以外保持布局 (模板) 和呈现 (CSS)。
{{< /hint >}}

使用基于标记的文档来存储数据有很多优点。 网页的大部分内容都是无结构的。 常规数据库将其保存在单个单元格中。 然而，这种方法并没有很好地利用数据库技术。 如果数据作为单个文件进行管理，我们可以使用像Git这样的版本控制系统来监视数据更改。 将数据与代码一起使用可以简化跨服务和构建环境的迁移。 我们可以将所有配置文件存储在一起。 优化和测试更加简单，能够创建新的构建环境(stage阶段、production阶段等)按需提供。 对于非结构化内容，数据库的大多数组织和查询功能都无济于事。 基于数据库托管博客或通用网页并不是对其资源的最佳利用。

随着Git和GitHub的普及，许多开发人员已经熟悉了标记语言，尤其是Markdown。 大多数开发人员用标记语言编写自述文件。 这些语言稳定、规范、易学、易懂。 有很多工具可以用这些语言编写或将数据迁移到这些语言。 它们还可以很好地使用diff和merge工具(用于比较文件中的更改)，并且大多数编程语言都有解析这些语言的库。 该工具为程序员以他们喜欢的方式操作数据提供了极大的灵活性。

{{< hint info >}}
**Exercise 1.2**

Jamstack中的M代表什么？
- a. markup
- b. Markdown
- c. MySQL
- d. MongoDB
{{< /hint >}}