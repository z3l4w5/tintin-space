---
weight: 3
title: "1.3 The JAM in Jamstack"
date: 2022-09-12T18:26:30+08:00
draft: true
---

# 1.3 The JAM in Jamstack

The JAM part of the Jamstack stands for JavaScript, APIs, and markup. Let’s take a look at each of these components.

## 1.3.1 JavaScript

JavaScript in Jamstack refers to all the approaches to client-side scripting that provide interactivity and dynamic functionality, which is personalized to the user and cannot    be precompiled. This enables developers to react to  user actions  and  modifies  the  user interface at run time. Jamstack leaves the specifics of the JavaScript framework  and its management to the web developer.

In traditional stacks, the server plays a prominent role in handling user interactions. It generates new pages even when just a part of the page needs to be modified. That is unnecessary and suboptimal. Modern JavaScript is fully capable of storing the user state in the browser. It can communicate with the server and update the interface without the user needing to reload or see a flicker in the interface. Jamstack pre- scribes using JavaScript for use cases where it shines the best—providing interactive interfaces to the end user and communicating from the client to the server.

## 1.3.2 Application programming interfaces (APIs)

Application programming interfaces (APIs) provide a well-defined contract for communicating with a web service. APIs abstract the entire server functionality so the client does not need to understand the server internals to consume the service. In Jamstack, pre- compilation and client-side JavaScript take over a lot of the work usually done on the server, but the server still has its use cases. These include storage of the application state across machines, computations that require more processing power than a single machine, and data that must be transmitted back from the website viewer to the servers. Many traditional systems expose APIs to communicate with the underlying func- tionality. Although this approach fits in the Jamstack definition, Jamstack advises min- imizing the building of APIs to reduce maintenance overhead. A lot of operations that need APIs in other stacks are handled differently in Jamstack. Instead of content cre- ation, update, or deletion APIs, you can place, update, or remove files on disk. Only dynamic updates based on user actions in the website (like purchases and comments)
need dedicated APIs.

There are third-party API providers that provide high-level APIs, which developers can use without going through the overhead of building everything themselves. From handling comments to full-text searches, a lot is available at scale without writing cus- tom code. When we need to write a custom backend, cloud service providers make that task easier than building it from scratch. With FaaS, the cloud service providers take over the ownership of uptime, ongoing security updates, and scaling with user load. The service provider maintains performance and availability across the globe. The developer writes code and hands it over to the service provider to deploy. The
ongoing work is minimal. Developers can then work to enhance functionality or update any dependencies at the function level.

## 1.3.3 Markup

The traditional definition of markup includes a set of annotations (like XML tags in HTML documents or stars around the text in Markdown) in a text document that pro- vides further information on how to understand or render the text. Jamstack consid- ers the entire markup document as markup. This consists of the textual data, the annotations, and the structured metadata.

Markup forms the data layer of the Jamstack. Unlike traditional databases, we store markup in text files. It is readable and editable by humans in its raw form without using a tool to convert it to a readable format. Markup languages provide a way to write formatted documents in a terse and readable way. Markdown is the most popu- lar markup language for writing content in the Jamstack. (We will examine Markdown in detail in chapter 3.) Various metadata languages that we use for additional informa- tion associated with the document can accompany this content. One of these is YAML (Yaml Ain’t Markup Language), which we will also discuss in chapter 3.

{{< hint warning >}}
**NOTE** HTML (HyperText Markup Language) is also a markup language, and you are free to choose that for writing your data in Jamstack. Human-readable languages like Markdown, however, make it easier to read and maintain our data. This is converted to HTML during rendering, keeping the layout (tem- plate) and presentation (CSS) out of content.
{{< /hint >}}

There are many advantages to using a markup-based document to store data. Most of the web page is unstructured. A regular database keeps it in a single cell. This approach, however, is not a good use of database technology. We can use a version control system like Git to monitor the data changes if the data is managed as individ- ual files. Having the data along with the code eases migration across services and build environments. We can store all configuration files together. Optimization and testing are more straightforward with the ability to create new build environments (stage, production, etc.) on demand. With unstructured content, most of the organization and querying capabilities of the databases are not helpful. Hosting blogs or generic web pages based on a database is not the best use of their resources.

With the popularity of Git and GitHub, many developers are already familiar with markup languages, especially Markdown. Most developers write readme files in a markup language. These languages are stable, standardized, easy to learn, and easy to understand. There is a lot of tooling available to write in these languages or migrate data to them. They also work well with diff and merge tools (used for comparing changes in a file), and most programming languages have libraries to parse these lan- guages. This tooling provides extreme flexibility for programmers to manipulate data the way they like.

{{< hint info >}}
**Exercise 1.2**

What does the M in Jamstack stand for?
- a. markup
- b. Markdown
- c. MySQL
- d. MongoDB
{{< /hint >}}