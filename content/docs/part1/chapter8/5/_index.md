---
weight: 5
title: "8.5 Getting a specific version of a theme"
date: 2022-09-12T18:26:30+08:00
draft: true
---

# 8.5 Getting a specific version of a theme

Hugo Modules has support for versions via Git tags. This allows us to link to a different version of our dependencies rather than what is the latest mainline. In many projects, mainline is under active development and unstable when a release version is marked separately. We will switch back to AcmeTheme with Hugo Modules. A copy of the AcmeTheme is on GitHub in the github.com/hugoinaction/AcmeTheme folder, tagged with version 0.8.0 for its contents through section 8.5 (this section) of the book.

{{< hint warning >}}
**NOTE** Do not use the main branch of the Acme repository on GitHub because it points to the AcmeTheme module at the end of this book.
{{< /hint >}}

To get a specific version of a theme, we need to specify the theme as we did before,   but instead of telling Hugo to automatically fetch the latest version via hugo server, we will manually tell Hugo the version to fetch. Let’s start by changing our theme to  the hosted AcmeTheme repository in our configuration as the following listing shows.

{{< details title="Listing 8.3 Switching to the AcmeTheme repository (config/_default/config.yaml)" open=true >}}
```yaml
theme: github.com/hugoinaction/AcmeTheme
```
{{< /details >}}

{{< hint warning >}}
**NOTE** The live server should not be running when updating to AcmeTheme, and we should not call hugo server at this point. It will lead to the installa- tion of the main branch of AcmeTheme.
{{< /hint >}}

Next, we need to install the theme from the v0.8.0 tag. There are two ways to do this: adding an entry to the go.mod file manually or running the installation command from the command line. The hugo mod subcommands are associated with Hugo Mod- ules, which provide access to the management features related to Hugo Modules. We use hugo mod init to define a new module that makes up our website. The hugo mod get command fetches the module-based dependencies manually. The -u command- line flag overwrites the existing entry in go.mod if present. The following listing adds an entry to the go.mod file for the v0.8.0 version.

{{< details title="Listing 8.4  Adding a specific version of AcmeTheme" open=true >}}
```shell
hugo mod get -u github.com/hugoinaction/AcmeTheme@v0.8.0
```
{{< /details >}}

With this command, you should see require github.com/hugoinaction/AcmeTheme v0.8.0 // indirect in your go.mod file. The checksum file, go.sum, should also include “v0.8.0” as the installed version of the AcmeTheme dependency.

We can continue to use our website with AcmeTheme linked as a module in Hugo. We have completely moved off Eclectic with this change and have taken over complete control of the Acme Corporation website with every piece of code in our possession. We will not be using Eclectic or Universal in the rest of this book. We can remove the entries that were specific to these themes in the configuration (except for the color and the  copyright  in  config/_default/params.yaml),  as  well  delete  the  assets/image/ background.svg, assets/image/logo.svg, content/data-driven.md, static/image/*, and static/favicon.ico files, which we do not use in the theme Acme. We can delete the themes/AcmeTheme folder if we want to, and the website will still continue to function.

{{< hint info >}}
**CODE CHECKPOINT**    https://chapter-08-03.hugoinaction.com, and source code: https://github.com/hugoinaction/hugoinaction/tree/chapter-08-03.
{{< /hint >}}