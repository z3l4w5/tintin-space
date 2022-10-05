---
weight: 7
title: "1.7 Why choose Hugo?"
date: 2022-09-12T18:26:30+08:00
draft: true
---
# 1.7 Why choose Hugo?

Hugo is one of the oldest static site generators and has continued to rise in popularity over time. Its creator, Steve Francia, has extensive experience with CMS and technical writing needs. His background includes building a closed-source CMS (Supersite)
that’s used by Major League Soccer and Priceline. He has deep experience with Magento and WordPress and has served on Drupal’s board of directors. He led the technical writing departments of both MongoDB and Docker. He took all of that experience, using the strengths of each of these systems, and channeled that into designing Hugo.
Hugo lies at the sweet spot between a tool like WordPress, which is built primarily for a nontechnical audience, and Rails or Express.js, which provide the power to gen- erate generic software but require ongoing maintenance. With Hugo, you get the flex- ibility of a custom theme with less maintenance than most other options and excellent performance. Hugo is for users who don’t mind getting their hands into the code and for those who need to have a life outside of their project.

{{< hint info >}}
**You are not alone**

Hugo is extremely popular in the industry. Websites like Bootstrap (https://getboot strap.com), Let’s Encrypt (https://letsencrypt.org), Smashing Magazine (https:// www.smashingmagazine.com), Netlify (https://www.netlify.com/), and 1Password Support (https://support.1password.com/) use Hugo at scale. Smashing Magazine migrated its website with thousands of pages from WordPress to Hugo because of Hugo’s performance and ease of use.
{{< /hint >}}

## 1.7.1 Hugo is fast

Hugo is the fastest feature-rich static site builder available. While we may not appreci- ate this when starting a project, this is extremely important in our day-to-day lives. Waiting for compilation or refreshes is a significant reason for developer frustration  and can mean a project’s death if it’s a hobby. Performance becomes even more criti- cal when technology modifications force us to go through a substantial change in our website template. For example, the advent of mobile devices brought death to many WordPress themes, where updating every aspect was so painful that developers gave  up. Moreover, a Hugo-based website continues to provide a respectable development performance even with a decade worth of content. A Hugo-based website’s facelift or rewrite is easier and more enjoyable than with any slower framework.

{{< hint info >}}
**Hugo and the Go language**

One concern people have is that adopting Hugo means learning the Go language. While this is true for other static site generators written in scripting languages, this is not true for Go-based applications. There is no need to learn Go or to understand how it works to be successful with Hugo. Just like people don’t need to learn C++ to use Windows or Photoshop, Hugo does not require any Go programming knowledge. This book does not have a single line of Go code. The Go programming language has built-in support for concurrency. Writing code with parallel execution is easier in Go than in many other programming languages used to build website generators. Hugo benefits immensely from Go’s speed without additional complexity.

Hugo’s users use the Go template language, which, despite the name, is a different language from Go itself. It allows us to write anything we want, including modules and functions, without dealing with a lot of complexity with multithreaded code. You may not even need the Go template language if you don’t plan to write a custom theme or a shortcode. You can write content in a markup language and pick a theme off the shelf to build your website.

Most other Jamstack-based website builders have a single-threaded, sequential-flow source language. This approach allows them to have plugins, but you pay massively in the form of performance. With the most significant features available in Hugo, there is no need to compromise on build performance and developer experience with a slow framework.

Go is among the newer languages (publicly released in 2009), but it has broken into mainstream development. It is a top-10 language in terms of adoption. Major projects including Docker and Kubernetes are written in Go. Also, most of the cloud is written in Go, including AWS, Azure, and Google Cloud Platform (GCP). Major enterprises including Google, American Express, and Dropbox use Go extensively.

Conveniently, Hugo’s creator, Steve Francia, also serves as the product and strategy lead for the Go programming language at Google. Consequently, Hugo is a project that is well understood by the Go team. It influences the programming language itself and can adopt the best of its features.
{{< /hint >}}

## 1.7.2 Hugo is stable

The core features of Hugo have been supported for a long time and are not likely to break. Any new additions make sure that these features are not disturbed and con- tinue to work as-is. In the early days of Hugo, development moved slowly as the team focused on getting the architecture right. This approach has paid off. Hugo is flexible and extensible to new features, and most releases do not break the thousands of web- sites built with it.

The Hugo development team believes in the continuous evolution of Hugo while maintaining backward compatibility. Hugo attempts to be backward-compatible across releases and guides us in upgrading if something needs to change. If you pick an old theme and get the latest version of Hugo, you might get some warnings, but most of it should continue to work.

## 1.7.3 Hugo is built for performance

The Hugo community has a tendency to look for performance gains in everything they do. There is a lot of advice on improving your website’s performance in easy-to- do steps in the community forums. If you find a random script from the internet for doing something with Hugo, there is a high likelihood that its author has optimized it for performance.

The core performance of Hugo also impacts its output. The performance primi- tives are available for other uses. Developers can learn from the approach that Hugo uses for optimizing their workflows.

## 1.7.4 Hugo is self-contained

A plugin-heavy system appears to provide a lot of flexibility and capabilities until main- tenance rolls around. Your site can get into a bad state even if one plugin is aban- doned while the framework is being actively maintained! Plugin abandonment has been a classic problem with frameworks like Rails, where each major version became a massive pain for migrating all the plugins. We can see the same in the ecosystems like Backbone and Angular, where there are many stale plugins. Even Jekyll, which is extremely popular and actively maintained, has a considerable problem of plugin rot.

Being self-contained has allowed Hugo to bypass issues that have plagued other projects. The core team has standardized  optimal approaches  to perform  tasks  that  are available natively. The Hugo team has optimized Hugo without needing lower-  level API compatibility. They continue to write complicated multithreaded logic for   the standardized workflows to eke out the few extra milliseconds that their users can spend elsewhere. Hugo’s users get a lot more support than they  would  from  the  plugin authors and have less fear of abandoning their core workflows.

Being self-contained does not mean Hugo is not extensible. The Go template lan- guage is potent, and users can share snippets of code as  modules that can be reused   and that can perform complicated logic using this language.

## 1.7.5 Hugo is a single file

Hugo packages all its core dependencies and resources in to a single executable file. A single file makes downloading Hugo, transferring it to another machine, and backing it up extremely simple. In systems where each file has a lot of scrutiny due to security concerns, a single binary file with no other dependencies shines. Developers can merge the Hugo binary with their source code to use it in a restricted environment. With a single file taking care of everything, there are no dependencies to update and no build systems to manage. The full web stack with custom APIs can be built with a handful of dependencies. This freedom is in stark contrast to JavaScript-based static site builders, which have hundreds of dependencies, each of which might need to be vetted by a security team for usage in an enterprise environment.

## 1.7.6 Hugo can be extremely low maintenance

With fewer moving parts (plugins and operating system dependencies), a tiny installa- tion footprint, no database, and no complicated hosting steps, the maintenance churn with Hugo can be a lot less than with other web development approaches. Each depen- dency needs to be maintained. You can get a compelling website with low maintenance with just Hugo and a hosting provider. While Hugo has had updates where backward compatibility has broken (for valid performance, extensibility, and maintainability reasons), you are free to take the updates when you have time, and you do not have to
fix arcane plugins. We cannot say this about most other ecosystems in the web develop- ment world.

## 1.7.7 Hugo can save you from analysis paralysis

Hugo is opinionated and built with a lot of techniques to get up and running quickly. While the powerful template system allows you to roll out a custom solution to a prob- lem, the Hugo team has already solved the most common ones. Hugo has generic implementations for pagination, categorizing content into unlimited types of catego- ries, and getting core website elements like menus. Getting up and running is easy    with Hugo because there is a well-documented and widespread approach to solving most problems readily available.

## 1.7.8 Hugo is powerful

Despite being opinionated, Hugo is versatile. The Go template language that Hugo extends is powerful and flexible. This power provides the ability for developers to write proper programs with Hugo. The standard library provided by Hugo is enormous and growing. It comes with outstanding performance right from the start. Even if you write terrible code, the core performance of the built-in functions ensures a relatively good performance for the website’s compilation. With access to APIs during website gener- ation, Hugo provides a lot of power without losing the generated output’s performance. You can write functions anywhere in your website with Hugo, including while developing content (as custom shortcodes embedded in the markup) to do some spe- cial processing. You can encapsulate that into something that you can reuse or leave as
one-time snippets of code on specific pages.

Hugo has lots of web development primitives. Still, not using them does not seem like fighting the framework. If you don’t want to use a feature provided by Hugo and build your own using the template language, the experience with the rest of Hugo does not deteriorate. Hugo provides good support for interacting with APIs and Java- Script that can provide extensibility and dynamicity where needed.

## 1.7.9 Hugo is scalable

Hugo already caters to websites with multilingual content, having thousands of pages and millions of monthly active users. Hugo has a proven record of handling the scale of some of the biggest and most heavily used websites on the internet. There are already enough primitives and capabilities to scale the Hugo-based website from a developer to a team. Hugo supports a wide variety of input and output formats. It has various features to enable the automation of the day-to-day work for a nontechnical member of the team.

## 1.7.10 Hugo is a community project

A community of volunteers maintains Hugo with no commercial interest in the proj- ect. This voluntary nature allows for the direction of the project to be in the commu- nity’s best interest. Hugo cannot pivot, get acquired, or shut down at the whim of a corporation.

![Figure1.5](Figure1.5.svg)

Figure 1.5 DevOps and the Jamstack: Alex, the web developer, talks to Bob, who works as a system/IT admin. Bob convinced management to use a cloud-based solution with the existing technology and drop the investigation into the Jamstack.
