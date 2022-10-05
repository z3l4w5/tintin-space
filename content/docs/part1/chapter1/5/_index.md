---
weight: 5
title: "1.5 When not to use the Jamstack"
date: 2022-09-12T18:26:30+08:00
draft: true
---

# 1.5 When not to use the Jamstack

One assumption of the Jamstack is that the content is available at compile time and does not change rapidly. The Jamstack does not offer a lot if this assumption turns out to be false. The following sections provide use cases for when not to use Jamstack.

## 1.5.1 When there is dynamic data with no historical significance

If we are building a dashboard-type application with ever-changing data, then precom- pilation as a concept does not provide great value. Sensor-based data  can  change within milliseconds. In many cases, no one reads this data. Jamstack  does not work  well with this type of application. A major exception is reporting, where some data needs to live for a long time, is read frequently, and is rarely, if ever, changed. This  type of report is a perfect case to be pre-generated and saved. There is no point in   doing this on the fly. The Jamstack fits the reporting use case perfectly.

## 1.5.2 Building based on user-generated content with transient data

Websites like Twitter and Facebook have tiny posts that we rarely read as individual pages. These get compiled into feeds, which are different for each user and which change over time. The users may not read the feed at any given time, so pre-generation can prove to be wasteful. These use cases do not fit into the write once, read many times scenarios the Jamstack excels at. While we could theoretically compile often-used pages, the traditional web stack can also do that. One thing to remember here is that the story changes considerably if the data has value in permanence. If we have user-generated blog posts, product pages, or articles that are written once and read many times, this comes back to the write once, read many times use case that the Jamstack is great at.

## 1.5.3 Having user-specific web pages

There are websites where the developers personalize each page for the user. This data is different because it’s based on the user ID. Therefore, it might not make sense to precompile. Most users might not log in. There is no public access to bots that can cause increased load. The whole concept of many reads and a single write for the data is false. An example of this would be a calendar application. Because each user’s cal- endar is different, it does not make sense to pre-generate everyone’s daily calendar.

## 1.5.4 When there is no data to compile

Web apps are websites where the user is a creator and a consumer. For a document editor (think Google Docs), there is no data to present. In these cases, the Jamstack approach does not help.

Note that the Jamstack is helpful in all the previous cases for building the static parts of the website. These include the Privacy Policy page and the Terms of Use page. Even the About Us page and the company blog can be built optimally using the Jam- stack. These pages could be set up using the Jamstack approach, while a different stack can serve the rest of the website or web application.

{{< hint info >}}
**Exercise 1.3**

Which website from the following list would be best to build with the Jamstack?
- a. A search engine
- b. A shopping website
- c. A social network
- d. An image editor
{{< /hint >}}