---
weight: 8
title: "1.8 Is speed really important?"
date: 2022-09-12T18:26:30+08:00
draft: true
bookToc: false
---

# 1.8 Is speed really important?

We cannot emphasize enough the importance of build performance. Hugo employs many techniques to speed up build times, like having a multithreaded core with support for caching at all layers to prevent as much rework as possible. Speed frees the developer from the burden of waiting for the build to complete after every small change.

If you launch Hugo in watch mode (a special mode for development), the website comes up in less than a second. It reloads with your edits without having to go through the entire step of setting up fancy hot module replacements for live reloads. This feature is not just for the themes but for the whole of the website! We get the flexibility to edit the website in the 5 minutes that we might have between other chores. In other frameworks, getting up and ready is in itself a task.

Because you don’t need to recompile your site after changes, the developer can make changes or experiment and see results quickly. The same is the case with data entry. A significant burden with static site builders and slow build times is that committing data is something that the content writer needs to plan for because getting up and running itself can take time. The flexibility of WordPress and the performance of the Jamstack are not either/or with a framework like Hugo.

With performance at Hugo’s core and all the primitives  exposed, as  a developer you start to rethink your website-building strategy. Does this code need to go into JavaScript that has to run on every one of the billion customer machines that visit this page, or can we write this so it runs once and saves the results as SVGs or precomputed HTML so that our customers don’t have to re-execute? These minor tweaks while building go a long way in improving the website’s performance.

{{< hint info >}}
**Exercise 1.4**

Hugo is built using which programming language?
{{< /hint >}}