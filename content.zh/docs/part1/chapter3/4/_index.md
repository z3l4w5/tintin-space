---
weight: 4
title: "3.4 元数据"
date: 2022-09-12T18:26:30+08:00
draft: true
---

# 3.4 元数据

通过使用格式化元素和结构修饰原始文本数据，页面在使用Eclectic主题呈现时看起来是完整的，这形成了与Markdown数据相关联的模板和代码。 虽然页面上有足够的内容来形成一个网站，但我们需要提供信息，我们可以用来组织内容，并在列表、菜单等中构建内容。 Markdown不是为此提供结构化数据的最佳语言。 Hugo支持另一组我们称为元数据语言的语言。 我们可以使用这些语言来提供此信息。 其中之一是YAML (https://yaml.org/)，我们在本书中使用它。 它是一种流行的软件配置语言，也是元数据语言中最容易阅读的。

YAML代表YAML Ain't标记语言 (YAML的Y代表YAML，递归首字母缩写)。 它是一种用于结构化数据的语言，键和值之间用冒号(：)分隔。 YAML的定义突出了一个事实，即YAML的核心用例是围绕结构化数据，而不是像我们在Markdown或HTML中那样标记数据。 YAML对空格敏感。 我们使用YAML作为Acme Corporation网站的配置文件。 YAML支持普通键-值对作为其主要数据结构，还支持单个数据元素和列表。 在本节中，我们将详细介绍YAML支持的语法和功能。

## 3.4.1 注释
我们对YAML中的注释使用井号标记 (#)。 注释是单行的，可以出现在YAML文档中的任何位置。 下面的清单显示了YAML注释的语法。

{{< details title="Listing 3.4   Adding YAML comments" open=true >}}
```yaml
# This is a comment.
```
{{< /details >}}

## 3.4.2 基本数据类型

为了人类的可读性，YAML会根据内容自动猜测数据类型。 它支持字符串、数字和布尔数据类型。 它还支持nil (也称为null) 类型。 如果键或值为true或false，YAML会自动将其强制转换为布尔数据类型。 它将数字猜测为数字，而其他一切都变成了一个字符串。 下面的清单提供了YAML的数据类型的示例。

{{< details title="Listing 3.5   Basic data types in YAML" open=true >}}
![Listing3.5](Listing3.5.svg)
{{< /details >}}    

## 3.4.3 多行字符串

YAML对缩进很敏感，换行符定义了新的YAML键值对的开头。 我们可以使用竖线字符(|)创建支持新行的多行字符串，使用大于号(>)创建对新行不敏感的多行字符串。 下面的清单提供了这方面的例子。

{{< details title="Listing 3.6  Using multiline strings with YAML" open=true >}}
![Listing3.6](Listing3.6.svg)
{{< /details >}}

## 3.4.4 列表

我们可以使用破折号 (-) 或方括号 ([]) 在YAML中声明列表。 下面的清单显示了如何添加列表。

{{< details title="Listing 3.7  Representing lists in YAML" open=true >}}
![Listing3.7](Listing3.7.svg)
{{< /details >}}

## 3.4.5 字典

词典也称为映射或对象，是键-值对。 顶级YAML对象也是字典。 我们可以在YAML中创建词典和子词典，它们可以包含所有类型。 下一个列表显示了如何使用YAML添加字典。

{{< details title="Listing 3.8 Representing dictionaries in YAML" open=true >}}
![Listing3.8](Listing3.8.svg)
{{< /details >}}

{{< hint info >}}
**Exercise 3.3**

YAML不支持以下哪种数据类型？
- a. Date
- b. Boolean
- c. Map
- d. List
- e. Numbers
{{< /hint >}}

## 3.4.6 重新审视config.yaml

现在是重新审视config.yaml的好时机，我们在第2章中创建了它，此后一直在修改它。 它包含baseURL和title等元素的键值对。 这些项的顺序并不重要。
author，menu和params元素是字典，而页脚和main是params和菜单字典中的列表。 因为类型是自动推断的，所以recentCount是一个数字，recents是一个字符串，而true会自动转换为布尔值。 清单3.9显示了配置文件中YAML元素的最新用法。

{{< hint warning >}}
**NOTE** 由于主菜单是一个列表，其中每个列表项都是一个词典，因此需要在config.yaml中的Main部分中的identifier前加上破折号。
{{< /hint >}}

{{< details title="Listing 3.9 YAML configuration for Acme Corporation (config.yaml)" open=true >}}
![Listing3.9](Listing3.9.svg)
{{< /details >}}