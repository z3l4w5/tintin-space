---
weight: 9
title: "8.9 Modules as template plugins"
date: 2022-09-12T18:26:30+08:00
draft: true
---

# 8.9 Modules as template plugins

We can share Hugo’s template code in the form of partials across multiple themes. These shared partials can act as plugins that wrap reusable functions. One module that can be useful when developing Hugo templates is the Hugo debug utilities, which provide the debug button we used with the Eclectic theme. We will add this module to the AcmeTheme module to be made available for all websites using this theme.

To use this module, we will import it in the config.yaml for AcmeTheme (https:// github.com/hugoinaction/hugoinaction/tree/chapter-08-resources/03).   Hugo   supports a single module and a list in the module: imports section in the configuration. Because we already have a module, we will need to convert module: imports into a list to get multiple modules as the following listing shows.

{{< details title="Listing 8.8 Importing the debug utilities (AcmeTheme/config.yaml)" open=true >}}
```yaml
module:
    ...
    imports:
        ...
        - path: github.com/hugoinaction/hugo-debug-utils
```
{{< /details >}}

Note that the Hugo debug utilities are already initialized as a Hugo module and provide its mounts internally. Therefore, we do not need to set the mounts for this module manually. We can start using this module in our code after inclusion. A copy of the Hugo debug utilities is also available in the chapter resources (https://github.com/ hugoinaction/hugoinaction/tree/chapter-08-resources/04).  In  the  base  template, layouts/_default/baseof.html, we can add the code in the following listing to load the debug bar after defining the footer block.

{{< details title="Listing 8.9  Adding the debug bar (AcmeTheme/layouts/_default/baseof.html)" open=true >}}
![Listing8.9](Listing8.9.svg)
{{< /details >}}    

{{< hint info >}}
**CODE CHECKPOINT**    https://chapter-08-07.hugoinaction.com, and source code: https://github.com/hugoinaction/hugoinaction/tree/chapter-08-07.
{{< /hint >}}

If we run the live server mode by issuing hugo server on the command line, the module is downloaded automatically, added to the go.mod and go.sum  files,  and  the  debug button should show up. Hugo Modules makes isolating Hugo dependencies simple. To understand how this works, we can take a look at the config.yaml file present in the hugo-debug-utils modules using this code:
```yaml
module: 
  mounts:
    -source: debug-bar/template
      target: layouts/partials/debug
    -source: debug-bar/css
      target: assets/css
    -source: debug-bar/js
      target: assets/js
    -source: console
      target: layouts/partials/console
```

The mounts for this module, including the JavaScript, CSS, and the partial, are specified in its configuration. The corresponding files are placed in the correct virtual locations by Hugo during website compilation.

The Hugo debug utilities also come with a console partial that we can use to log any Hugo variable in the browser’s JavaScript console. This is extremely useful when developing templates. Say that we want to know the value of an expression. We can pass this to the console partial, and the value of the expression will be made available in the browser console. The following listing allows us to view the front matter parameters passed to the page (use AcmeTheme/layouts/_default/baseof.html to make these changes).

{{< hint warning >}}
**NOTE** You should only add the code in the following listing when debugging.
{{< /hint >}}

{{< details title="Listing 8.10  Passing debugging parameters the browser console" open=true >}}
```
{{ partial "console" .Params }}
```
{{< /details >}}