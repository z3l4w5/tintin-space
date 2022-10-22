---
weight: 8
title: "8.7 Modifying dependencies locally"
date: 2022-09-12T18:26:30+08:00
draft: true
---

# 8.7 Modifying dependencies locally

We can change the contents of the _vendor folder and view the changes live in Hugo, but this is a bad practice. The next time we update a dependency, our changes will get overridden. Pushing every commit to the theme repository can also be tiresome. Hugo has a mechanism to provide a local version of a hosted dependency for local development. We need to set up the dependency (the AcmeTheme in this case) as a Hugo module to enable this. To perform this task, go to the theme folder and run the following command:

```shell
hugo mod init AcmeTheme (Initializes the module with the name AcmeTheme)
```

This command creates a go.mod file in the theme’s folder. With this change, the module system can read the AcmeTheme as more than a folder, but as a proper Hugo module. Next, we can provide the path to this module in go.mod for the Acme Corporation website using the replace directive under the require call as the following listing shows.

{{< details title="Listing 8.5 Adding the path to AcmeTheme for local development (go.mod)" open=true >}}
```
module AcmeCorporationWebsite

...

replace github.com/hugoinaction/AcmeTheme =>
    <Absolute or relative path to the theme>.
```
{{< /details >}}

With this replace directive, we can easily continue developing locally in an independent repository and still refer to it using Hugo Modules. In the code samples present with this book, we will use the AcmeTheme folder in the code repository to host the theme. Only the final version of the theme (at the end of the book) is pushed to the github.com/hugoinaction/Acme folder. Because the _vendor folder is present, the replace directive will not take effect until we delete the _vendor folder, which has higher precedence. We should use the _vendor folder for archiving and not development. Although it is good to use this when the theme does not change (only the content changes), it is a hindrance when we develop the theme, so we will delete it.

We have created a new module we plan to use outside of the Acme Corporation website. It is a good idea to declare its requirements so other places can import it. Hugo’s package management needs two files: the go.mod and the config. The go.mod file lists dependencies, and the config file provides configuration and package information.

Because AcmeTheme does not have a colossal configuration yet, a config folder will be overkill. We will place a simple config.yaml in the theme’s folder (https:// github.com/hugoinaction/hugoinaction/tree/chapter-08-resources/01). In the configuration, we can specify the minimum and maximum versions of Hugo that this specific module depends on and whether Hugo extended is needed. Although it is not required, it is a good idea to specify a minimum version of Hugo that the theme needs. We do this in the following listing.

{{< details title="Listing 8.6 Specifying the minimum version of Hugo (AcmeTheme/config.yaml)" open=true >}}
```yaml
module: 
  hugoVersion:
    min: 0.91.2
```
{{< /details >}}

{{< hint info >}}
**CODE CHECKPOINT**    https://chapter-08-05.hugoinaction.com, and source code: https://github.com/hugoinaction/hugoinaction/tree/chapter-08-05.
{{< /hint >}}