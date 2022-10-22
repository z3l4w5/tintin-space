---
weight: 1
title: "5.1 Separating data and design"
date: 2022-09-12T18:26:30+08:00
draft: true
---

# 5.1 Separating data and design

To control the website’s index page with a markup document, we need to create the markup document first. The content folder is the branch bundle for the entire website. We need to place _index.md   (https://github.com/hugoinaction/hugoinaction/tree/chapter-05-resources/01) in that folder to represent the /index.html web page. Note that if we use index.md instead, the website’s root becomes a leaf bundle and will not use the template we provide in the layouts folder. With the markup document present, we can move the data currently hardcoded in index.html into the front matter of this markup document. The following listing shows the contents of the index page using Markdown as the markup language. We’ll use this information in the index.html page.

{{< details title="Listing 5.1  The contents of the index page in Markdown (content/_index.md)" open=true >}}
```yaml
---
title: Acme Corporation 
description: Welcome to the website of Acme Corporation, the 
 leading creator of digital shapes on the planet, providing 
 precise shape creations that are ready to use. 
subtitle: shaping the world for you to live in 
explore: blog 
---
```
{{< /details >}}    

## 5.1.1 Accessing the Go template language

Hugo uses the Go template language, which is different than the Go programming language, for creating templates. The Go template language can be accessed with the HTML in the template pages by using double curly braces ({{ … }}), which are also called mustache tags.

Appendix D provides a short overview of the Go template language. The resources for this chapter also include a folder named template-playground that we can place in the layouts folder and play around with Hugo’s template technology. The corresponding changes can be viewed from the /template endpoint if we place template.md in the  content  folder  (https://github.com/hugoinaction/hugoinaction/tree/chapter-05-resources/02). While this book introduces most of Hugo’s commonly used features, if you are looking for a more comprehensive list of its features (outside of the appendix), Hugo’s official  documentation  at  https://gohugo.io/documentation/ does a great job of listing these.

Hugo treats the content outside of the mustache tags as a raw string that we can pass in to the final HTML as is. All the information present in the content folder is also available via variables in the template. Hugo provides a few top-level variables to access content, including:
- $—This variable represents the top-level context of the template. In the case of a page template, this variable represents the current page. Page-level metadata like the title is available as $.Title, and the description is available as
$.Description. A page-level variable links to itself via the Page property, and we can therefore write the website’s title as $.Page.Title.
- site—This variable provides data for the whole website. We can use this variable to access configurations in config.yaml, to navigate the website’s pages via site.Pages, to move through the taxonomies using site.Taxonomies, and to view custom parameters with site.Params.
- hugo—This variable provides access to the Hugo compiler. The compiler includes methods like hugo.IsProduction (to detect if we are building for production) and hugo.Version (to inform us about the Hugo version).

{{< hint info >}}
**Exercise 5.1**

A shortcode in Hugo also allows for Go templates. What would the top-level context $ represent in a shortcode?
- a. The shortcode
- b. The containing page
- c. The entire site
- d. None of the above
{{< /hint >}}


The metadata provided in the front matter is available in the page-level variable accessible as $ or $.Page. In addition, the page-level variable has multiple properties and subproperties that we can use to access user-supplied and Hugo-generated metadata about the page. We can use these in the template for the index page (layouts/ index.html) by using the page-level variables $.Title and $.Description. The following listing provides the page-level variables that we’ll use to fill the website’s <head> section.

{{< details title="Listing 5.2 Using page variables (layouts/index.html)" open=true >}}
```html
<head>
<meta charset="UTF-8">
<meta name="description" content="{{$.Description}} ">
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<link rel="stylesheet" href="./index.css">
<title>{{$.Title}}</title>
</head>
```
{{< /details >}}   

We can reuse the page title in the body of the index page. That way, we do not need to repeat this information across web pages. The following listing shows how to access the same parameter multiple times in a Hugo template to reuse the page title.

{{< details title="Listing 5.3 Accessing the same parameter (layouts/index.html)" open=true >}}
```html
<h1>{{$.Title}}</h1>
```
{{< /details >}}

Hugo standardizes the title and description properties of the web page. These are available in the top-level page object. The custom metadata item subtitle is not available at the top level in Hugo. To access the subtitle variable, we need to use the Params object in the page. That way the Params object holds all the user-defined metadata in the front matter. By moving all the custom metadata to the Params object, the Hugo team was able to add more properties to the page variable without breaking compatibility with older websites. The following listing shows how to access the subtitle variable in the Params object.

{{< details title="Listing 5.4  Accessing nonstandard parameters (layouts/index.html)" open=true >}}
```html
<h2>{{$.Params.Subtitle}}</h2>
```
{{< /details >}}

{{< hint warning >}}
**NOTE** Although we defined the metadata item as subtitle, in the listing, we accessed it as Subtitle. Variables in $.Params are not case-sensitive. The supplied title also exists in Params and can be accessed as $.Params.Title.
{{< /hint >}}

{{< hint info >}}
**CODE CHECKPOINT**     https://chapter-05-01.hugoinaction.com, and source code: https://github.com/hugoinaction/hugoinaction/tree/chapter-05-01.
{{< /hint >}}

## 5.1.2 Existence checks

Although our code provides the data needed, there are edge cases where the code will fail. One rule of thumb when writing markup-driven websites is to assume all properties are optional. That  enables  all the content to be portable. If the user switches from  a different theme to a more current one, they have an intense desire that the website remains functional at all times. They can slowly provide the data to support themespecific features. If we do not provide any metadata, the home page we just created renders empty strings in place of all the custom data. But we can do better by providing default values and running existence checks.

Listing 5.5 provides one way to do an existence check using the if statement in Hugo. In the listing, the if statement checks its arguments for a truthful value for the title, description, and subtitle. When the supplied argument is true, the if statement executes the template code inside the if block. Additionally, the container HTML  tags are not present if we do not provide the inner content. The values that fail the if check include false, 0, a nonexistent variable (nil), a slice, a map, or a string of length zero.

{{< details title="Listing 5.5  Using existence checks (layouts/index.html)" open=true >}}
```html
...
{{if $.Description}}
<meta name="description" content="{{$.Description}}">
{{end}}
...
{{if $.Title}}<title>{{$.Title}}</title>{{end}}
...
{{if $.Title}}<h1>{{$.Title}}</h1>{{end}}
{{if $.Params.Subtitle}}<h2>{{$.Params.Subtitle}}</h2>{{end}}
...
```
{{< /details >}}

{{< hint info >}}
**CODE CHECKPOINT**	https://chapter-05-02.hugoinaction.com, and source code: https://github.com/hugoinaction/hugoinaction/tree/chapter-05-02
{{< /hint >}}

## 5.1.3 Using site variables for defaults

The page title is also optional. If we do not provide the title for the home page, we can fall back to the website title supplied in the config.yaml file. The following listing  shows how we can achieve this by using the site.Title variable for the content if the page title is unavailable. We can use the else logic for falling back to site.Title.

{{< details title="Listing 5.6  Falling back to the website’s title (layouts/index.html)" open=true >}}
```html
{{if $.Title}}
<title>{{$.Title}}</title>
{{else if site.Title}}
<title>{{site.Title}}</title>
{{end}}
```
{{< /details >}}

{{< hint info >}}
**CODE CHECKPOINT**	https://chapter-05-03.hugoinaction.com, and source code: https://github.com/hugoinaction/hugoinaction/tree/chapter-05-03.
{{< /hint >}}

We can also use $.Site for the site variable. Because site is available globally in the Hugo templates to access all the site variables, it is advisable to use site instead of
$.Site. That’s because $.Site may not be available across all template types.

## 5.1.4 Creating variables for simplification

Although the page title is needed twice on the home page, that is an unnecessary repetition. We could store the title in a variable called $title and use that instead as the following listing demonstrates.

{{< details title="Listing 5.7  Declaring $title with a default value (layouts/index.html)" open=true >}}
```html
{{$title := $.Title}}  Declares a variable called $title
```
{{< /details >}}    

Note that all user-defined variables start with a dollar sign ($). A declaration also requires := for assignment. We can use a single equals sign (=) for future assignment as well. If needed, the following listing shows how we can provide a fallback value to a Hugo variable.

{{< details title="Listing 5.8  Using if to provide a fallback value (layouts/index.html)" open=true >}}
```html
...
{{if not $title}}
{{$title = site.Title}}
{{end}}
```
{{< /details >}}

In the listing, if not checks if the page title is not truthful and, if so, resets the $title variable to the website title. In the Go template language, not is a Boolean function. It takes a parameter and flips its truthfulness.

Note that we can use = to reset an existing variable and := to declare a new one. Hugo scopes variables to the code block where they are present. In other words, a variable declared inside an if block is not accessible outside of it. Because we defined
$title with a default value earlier, we did not need the else statement to match the
if statement in the previous listing.

Also note that we cannot use variables without declaring them. Using a variable before declaration fails. Because we declared the title variable in listing 5.7, we can now use $title wherever we need the page title with the site title as a fallback. The following listing shows this usage.

{{< details title="Listing 5.9  Providing the web page title (layouts/index.html)" open=true >}}
```html
{{if $title}}<title>{{$title}}</title>{{end}}
```
{{< /details >}}   

{{< hint info >}}
**CODE CHECKPOINT**	https://chapter-05-04.hugoinaction.com, and source code: https://github.com/hugoinaction/hugoinaction/tree/chapter-05-04.
{{< /hint >}}

## 5.1.5 Using standard library functions to reduce the code size

Although we are not doing anything special to get the title, our code can be needlessly lengthy and challenging to write and understand. Hugo has predefined functions for common code patterns in its websites. These can significantly reduce the complexity of the templates and their code size. We got a taste of Hugo’s functions by using the not function in listing 5.8. Let’s look at another Hugo function next.

We can use the default function to provide a default value if a value is absent. We
can replace the if check with the usage of the default function. The following listing uses default as a shortcut to provide a default title for our website.

{{< details title="Listing 5.10  Declaring a default title (layouts/index.html)" open=true >}}
```html
{{$title:= default site.Title $.Title}}
```
{{< /details >}}    

Hugo functions separate their parameters with spaces. Function calls can be wrapped with parentheses, (). Unless we use multiple nested functions where there is ambiguity, parentheses are optional when invoking Hugo functions. We can write the not call in listing 5.7 as if (not $.Title), and the bracketed version of the default call would be (default site.Title $.Title).

The first argument to the default function is the default value, while the second is the value to be checked and used if it exists. One difference between default and the regular if check is that default checks for the existence of a value, whereas if verifies the value’s truthfulness. Empty strings, false, and 0 will not pass the truthfulness test. The if statement will also check the else code block if such is available. (This is only valid for the subtitle field. Note that Hugo provides Title as a string property and coerces false to the string "false", which is truthful for $.Title). To match the default behavior with the if statement, we should use the isset function. The following listing uses this function to check if a variable is not undefined.

{{< details title="Listing 5.11  Using the isset function (layouts/index.html)" open=true >}}
```html
{{if isset $.Params "subtitle"}}<h2>{{$.Params.subtitle}}</h2>{{end}}
```
{{< /details >}}

If we pass false as the subtitle of the web page (by setting subtitle: false in the front matter of the .md file), Hugo still renders the web page.

Another function worth mentioning here is $.Param. This function is tied to the
$ object because it accesses site.Params and $.Params. The pattern of accessing the page variable and falling back to the site variable is so common that Hugo has a built in method to do this. We can use $.Param when passing just the subtitle call to access the title. The following listing shows how to declare the $.Param function to provide the subtitle. The $.Param function provides the page subtitle and falls back to the site subtitle if the page subtitle is not present.

{{< details title="Listing 5.12  Using the $.Param function (layouts/index.html)" open=true >}}
```html
{{$.Param "subtitle"}}
```
{{< /details >}}

{{< hint info >}}
**CODE CHECKPOINT**	https://chapter-05-05.hugoinaction.com, and source code: https://github.com/hugoinaction/hugoinaction/tree/chapter-05-05.
{{< /hint >}}

{{< hint info >}}
**Exercise 5.2**

It is a good practice to continue to render a website even if certain front matter properties are absent. The___function allows us to fill in a custom fallback value if the front matter entry does not exist.
{{< /hint >}}

## 5.1.6 Using a context switch via the with conditional for simplifying further checks

Having deeply nested properties in objects like site.Params makes the template lengthy and difficult to read (and write). This verbosity discourages users from properly grouping their keys, which impacts website maintainability. For example, we provided site.Params.Footer[0].title as a property to the Eclectic theme. One can easily imagine why we would not want to write this line five times in code. Hugo provides a special context variable, a dot (.), to solve this problem.

The context variable can be loosely compared to the this variable in object-oriented programming languages, which becomes the method’s object. When rendering a page, the context variable represents a page, but if we are rendering a taxonomy, it becomes that taxonomy. If we render a shortcode, the context variable becomes that shortcode. When working in the context of a property, we can override the context variable with that property and access that property with the . variable.

Hugo provides the with conditional, which overrides the context variable in its
code block. Using with, we can write a less verbose existence check. That’s because with calls its inner code block if the variable is supplied with a value. We can pass a variable or an expression to with. If it evolves to a truthful value (not nil, 0, false, or an empty slice, dictionary, or string) that value is set as the value of . (the dot) inside the block contained in the with statement. In case the value is not true, the with block is skipped. The following listing shows how to override the context variable  using `with`. The . represents the value of the variable passed to with.

{{< details title="Listing 5.13 Overriding the context variable (layouts/index.html)" open=true >}}
{{with $title}}<title>{{.}}</title>{{end}}
{{< /details >}}

Inside the `with` code block, the context variable  . was replaced with the value of  the
$title variable. Note that if we do not set $title, this code does not execute. However, if we provide an else code block in the with block, Hugo runs that code instead.

{{< hint info >}}
**CODE CHECKPOINT**	https://chapter-05-06.hugoinaction.com, and source code: https://github.com/hugoinaction/hugoinaction/tree/chapter-05-06.
{{< /hint >}}

$ is by default the top-level context variable, but we can remove an unnecessary $ sign from our code to convert it into something that a typical Hugo theme developer would write. $ is only needed if we need to access the top-level context in the with block.

{{< hint info >}}
**Exercise 5.3**

When should with be used in a Hugo template?
- a. with is among the “bad” parts of Hugo, having a vast negative performance impact, and should not be used.
- b. with can be used to check the existence of a value and provide a default behavior or value if one is absent.
- c. with can be used to update the context to write less code if it relies only on the subproperties of a variable.
- d. with can be used to provide inline handling of map properties without having to write a nested function like index to access the property.
- e. both b and c.
- f. both c and d.
- g. b, c, and d.
{{< /hint >}}

## 5.1.7 Adding content processing

In this section, we will enhance the home page with more Hugo features to make it match the design shown in figure 5.2. The subtitle field we have rendered so far is in plain text. We want to start that with a capital letter and provide the capabilities to use Markdown-based formatting for the subtitle. Because the subtitle is already available   in a variable, this task involves passing the subtitle to an appropriate function to do further processing. To enable the subtitle to start with a capital letter, we can give this  to the humanize function as the following listing shows.

{{< details title="Listing 5.14  Adding the humanize function (layouts/index.html)" open=true >}}
```html
{{with .Param "subtitle"}}<h2>{{humanize .}}</h2>{{end}}
```
{{< /details >}}

After “humanizing” the subtitle, we can further use Markdown processing by passing the data through the Markdown parser via the markdownify function. In section 3.1.4, we discussed how the theme authors can parse Markdown from front matter data; markdownify is the function to do this. The following listing shows how to add this function for future Markdown support.

{{< details title="Listing 5.15  Adding the markdownify function (layouts/index.html)" open=true >}}
```go
{{with .Param "subtitle"}}<h2>{{markdownify (humanize .)}}</h2>{{end}}
```html
{{< /details >}}   	

{{< figure src="Figure5.2.svg" title="Figure 5.2 The Acme Corporation home page, where we used Markdown on the subtitle, and markup to control the index.html page in the layouts folder" >}}

Although calling nested functions using parentheses is a perfectly valid approach, Hugo also supports the pipe operator (|) for a more functional programming style. This allows us to take the output of the previous function and pass it to the next one. The following listing shows how to pipe though functions.

{{< details title="Listing 5.16  Using the pipe operator (layouts/index.html)" open=true >}}
```html
{{with .Param "subtitle"}}<h2>{{. | humanize | markdownify}}</h2>{{end}}
```
{{< /details >}}

The functional programming-style approach is easier to read and is preferred when the function takes just one argument. We will use this as an opportunity to make the words “world” and “live in” bold in the subtitle by wrapping them with double stars (**) as the following listing shows. We also need to link the Explore button using the explore option in the front matter for the index page to make that page data driven.

{{< details title="Listing 5.17  Highlighting parts of the subtitle (content/_index.md)" open=true >}}
![Listing5.17](Listing5.17.svg)
{{< /details >}}    

The ref function in Hugo takes a file or folder name and provides the corresponding URL for this content. We can also use relref for a relative path. The following listing calls the ref function to convert a file to the corresponding URL.

{{< details title="Listing 5.18  Using the ref function (layouts/index.html)" open=true >}}
```html
<a href="{{ref . (.Param "explore")}}"
>Explore</a>
```
{{< /details >}}

{{< hint info >}}
**CODE CHECKPOINT**	https://chapter-05-07.hugoinaction.com, and source code: https://github.com/hugoinaction/hugoinaction/tree/chapter-05-07.
{{< /hint >}}

## 5.1.8 Adding Markdown content

We have Markdown content in the content file. This content is available in its HTML form via the .Content variable on the root context ($) variable. We can place this anywhere on the page using {{.Content}} in our template to enable a new section on the home page as figure 5.3 illustrates.

{{< figure src="Figure5.3.svg" title="Figure 5.3 Adding Markdown content to the home page. (Photo for the about image by Angela Pencheva on Unsplash; photo for the contact image by Cristofer Jeschkeon on Unsplash.)" >}}

Let’s add some Markdown data to the Acme Corporation’s website’s home page (https://github.com/hugoinaction/hugoinaction/tree/chapter-05-resources/03).  The  following listing provides the data for the index page.

{{< details title="Listing 5.19 Adding descriptive content in Markdown (content/_index.md)" open=true >}}
```markdown
Acme is the **best**
==================

![about us](about.jpg) The finest in this field

Acme Corporation&trade; is the _ world's leading manufacturer of digital shapes_. From squares and circles to triangles and
hexagons, we have it all. Browse through our collection of various forms with different thicknesses and line styles.

[About Us](./about)

* * *

![contact us](contact.jpg) Personalized especially for you

We convert dreams into designs. Our artists are one of a kind.
We provide full support for customizing your designs with multiple contact sessions to understand your problems and get a satisfying result.

[Talk to us today](./contact)
```
{{< /details >}}

To use this content, we will also need two images, contact.jpg and about.jpg, which can be placed in the page bundle for the website index in the content folder. To fit the design of the current website, we will add the ID intro to the current section and create a new section with the ID description in the Markdown content. The following listing shows how this is done.

{{< details title="Listing 5.20 Rendering the Markdown content (layouts/index.html)" open=true >}}
```html
<section id="intro">
...
</section>
<section id="description">
{{.Content}}
</section>
```
{{< /details >}}

{{< hint info >}}
**CODE CHECKPOINT**	https://chapter-05-08.hugoinaction.com, and source code: https://github.com/hugoinaction/hugoinaction/tree/chapter-05-08.
{{< /hint >}}

Hugo automatically runs this content provided in the Markdown file through the Markdown parser and provides an HTML string to place directly in the document.

{{< hint info >}}
**Customizing the generated HTML from Markdown**

While generating HTML from Markdown, Hugo provides the developer with the flexibility to customize the HTML generated for a specific element. Special templates, called render hook templates, can control exactly how this rendering happens. For example, we can use the custom templates at layouts/_default/_markup/render-image.html, layouts/_default/_markup/render-link.html, or layouts/_default/_markup/ render-heading.html, and then decide on how to render the inline images, links, and headings provided in Markdown.

These templates have access to the entire set of page and site variables, along with unique variables like .Level, .Text, .Title, and  for the HTML headings, display text, appended title, and the provided URL in Markdown. In chapter 6, we will create custom render hooks to control Markdown rendering.

Note that the templates in the _default folder apply to the whole website. We can limit these to a set of pages by moving these templates to a specific content type. We will discuss content types in chapter 7. Developers can further process the generated HTML string using methods like findRE to replace certain substrings.
{{< /hint >}}