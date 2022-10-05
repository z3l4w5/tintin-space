---
weight: 4
title: "1.4 Why use Jamstack?"
date: 2022-09-12T18:26:30+08:00
draft: true
---
# 1.4 Why use Jamstack?

Prebuilding HTML content presented to the user has unique advantages—from mini- mal operations to outstanding performance and cost reductions. We’ll look at these advantages and more in the following sections.

## 1.4.1 Minimal operations

Because content is prebuilt before publication, the number of moving parts in a site is reduced. The service provider takes care of security updates, hardware failures, and network issues. The cloud host provides almost 100% uptime without any active involvement from the website owner. There is no need to be on call, no need to think about servers, scaling, load balancing, uptime across continents, or any other opera- tional overhead. The developer can focus on the joy of building, and the business can focus on its core competency rather than setting up a DevOps team.

## 1.4.2 Great performance

CDN hosts in its entirety the prebuilt HTML provided as a static website. This way, every file is cached and served from a server geographically close to the end user.  There is no round trip to an application server and no database query, which can  become a bottleneck. Most site generators targeting the Jamstack generate the HTML   at compile time. It is already available to render when the user requests it. The website is functional, even with a single HTTP request. A simple website built with Jamstack can provide a 90%+ performance score on most audits. If the developer is sensitive to performance while building the theme, the Jamstack-based website can meet all the criteria for a 100% score in these audits.

## 1.4.3 Lower costs

The removal of the database and the application servers from the hosting stack reduces the hardware costs. With the operations becoming automatic, most DevOps requirements are not present. All this translates to significant cost savings. You can have a website for free using static-site hosts like GitHub Pages and Netlify. All major cloud providers like AWS S3, Google Cloud Storage, and Azure Storage provide low- cost static hosting. There is no need to have an IT or a DevOps team for managing the fleet of servers.

## 1.4.4 Developer productivity

A version control system like Git manages a Jamstack-based website. There is no need to have complicated development environments. Running the code on the developer machine is one command away. Most websites can be deployed by a simple push to a server many times a day. These features give the developer the time and flexibility to focus on the content of the website.

## 1.4.5 Longevity

HTML/CSS is the most stable technology built. Today’s browsers bend over backward to continue to support all features that they have  supported since  the  1990s. If  you host a Jamstack-based website and vanish from the internet for a decade, it will still be there when you come back in the same state (mostly) where you left it. The internet is not forgiving to any technology stack outside of plain HTML, CSS, or JavaScript  hosted on a static server. You can even continue to use the static site generator in a vir- tual machine without updating the version. Because the generator is local, security vulnerabilities  in  the generator do not impact the website. You do not need to go  online and expose these vulnerabilities to the internet.

## 1.4.6 Tooling

With fewer moving parts and a well-defined structure, the tooling for Jamstack is much more advanced and powerful than other web stacks. One-click deployment is readily available with hands-off support for scaling through Netlify, GitHub Pages, and so on. Having the entire website present as code also means that there is nothing to hide. There are no complicated configurations for security or performance, no extra management overhead for different layers in the stack, and no IDE (integrated devel- opment environment).

{{< hint info >}}
**Updating on the fly**

When new to the Jamstack, it may seem to be a limitation that we cannot update the website on the fly. Most traditional systems provide an admin mode to update the website. The Jamstack does not prescribe anything. With the Jamstack, there is no need for any special tooling to update a Jamstack-based website.

The markup language is friendly and easy to use. We can provide updates in any text editor. Most version control providers like GitHub, GitLab, and Bitbucket can commit new changes from the browser. Continuous integration can automatically build and deploy this to production. We get the benefits of having an entire version control sys- tem for our content. We also can choose our text editor freely. As a bonus, we can update the theme wherever and whenever desired. Textual content, automatic deployment, and continuous integration ensure that we do not miss WordPress’s admin mode, but admin tools are also available if needed. We’ll discuss the Netlify CMS in appendix C.
{{< /hint >}}