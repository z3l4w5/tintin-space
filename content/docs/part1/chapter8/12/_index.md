---
weight: 12
title: "8.12 Commonly used Hugo Modules APIs"
date: 2022-09-12T18:26:30+08:00
draft: true
---

# 8.12Commonly used Hugo Modules APIs

Running hugo mod provides a great variety of subcommands that are useful in manag- ing modules in our daily life. For example,
- hugo mod tidy—Removes unused entries from the go.sum and go.mod files (like getting rid of Eclectic).
- hug mod clean—Clears the module cache to pick up newer changes (if done locally). Sometimes, the local store may get corrupt, giving us incorrect data.
- hugo mod graph—Shows the list of dependencies of the current website or mod- ule. Understanding go.sum can be challenging, but hugo mod graph makes this file human-readable.
- hugo mod get -u—Updates all modules.
- {hugo mod get -u ./...}—Updates all modules and their dependencies.
- hugo mod get <module>@<version>—Gets a specific version of a module.

Remember that we added the Eclectic theme as a module to try it out when we started with Hugo Modules. It is still present in go.mod and go.sum. It is costing us the need- less waste of bandwidth by downloading when we are not using it. We can use hugo mod tidy to eliminate unused entries from the go.mod and go.sum files.

{{< hint info >}}
**CODE CHECKPOINT**    https://chapter-08-10.hugoinaction.com, and source code: https://github.com/hugoinaction/hugoinaction/tree/chapter-08-10.
{{< /hint >}}

After cleaning up the dependencies, the correct dependency list can be viewed with hugo mod graph as listing 8.14 shows. This command provides a list of dependencies actively used in a Hugo website.

{{< hint info >}}
**Exercise 8.4**

True or False: Hugo Modules are automatically downloaded every time we build a Hugo-based website.
{{< /hint >}}

{{< details title="Listing 8.14 Getting the Acme Corporation website’s dependency list" open=true >}}
```shell
> hugo mod graph
AcmeCorporationWebsite github.com/hugoinaction/
➥ TermsAndPrivacy@v0.0.0-20200223231951-1c7c1972007a AcmeCorporationWebsite github.com/hugoinaction/
➥ AcmeCommon@v0.0.0-20210710221623-ca55f92c01bc AcmeCorporationWebsite github.com/hugoinaction/
➥ AcmeTheme@v0.8.0 => <path>/AcmeTheme github.com/hugoinaction/AcmeTheme@v0.8.0 github.com/hugoinaction/
➥ AcmeSupport@v0.0.0-20210710141629-d5aef37e0e9c
github.com/hugoinaction/AcmeTheme@v0.8.0 github.com/hugoinaction/
➥ hugo-debug-utils@v0.0.0-20200427035302-d4636e5c27cf
```
{{< /details >}}

{{< hint info >}}
**TIP** When running the development server, if you face errors that are unre- lated to the website’s code, Hugo’s module cache has likely gone bad. Hugo keeps its cache in the temporary data folder so that the operating system can reclaim the space if needed. Because this data is publicly accessible, it can get corrupted, leading to weird errors. When facing such issues, the best solution is to clear the cache entirely with hugo mod clean. Hugo re-fetches the data on the next launch.
{{< /hint >}}

This chapter completes the first part of Hugo in Action. In the second part of the book, we will move out of the bounds of the fully static website and see how Hugo interacts with the rest of the Jamstack. We will continue to complete the Acme Corporation website with a contact page, a JSON-based API, a small search engine, and then create an e-commerce area in our website using Hugo. We will discover some hidden gems in the Hugo template language and its features that do a lot more than what appears on the surface as we continue to introduce and learn more Hugo features to simplify web development.