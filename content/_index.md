---
title: "foreword"
---

![Cover](Cover.png)

# foreword

Hugo was born out of two beliefs: 1) website maintenance (authoring, hosting, secur- ing, etc.) could be dramatically simplified, and 2) the Go programming language and its ecosystem would provide the right base for a fast, straightforward, and productive website engine.

As I write this in late spring of 2022, we’re approaching the ninth anniversary of Hugo’s first public announcement (June 2013). Reflecting back to the months lead-    ing up to Hugo’s first release, I had recently begun investigating a new programming language from Google, the Go programming language. It had just reached 1.0 status, and I was looking for a project so I could learn through building. Simultaneously, I    was becoming increasingly frustrated with my WordPress-powered blog that was grow- ing in cost and complexity. I calculated that I had spent more time doing mainte-    nance and security patches than authoring new posts.

I had begun playing with the static site generators available at the time; Jekyll and Pelican being the two most prominent. Installing was complicated, however, taking me a few hours each because they both required me to first install the entire toolset for each programming language and then all the language dependencies. After that, I needed to install the software and all of its dependencies, requiring hundreds of pack- ages to be fetched and resolved.

I began porting my content to Markdown and building my blog in Jekyll. Render- ing my small blog of maybe 200 posts and the most basic template still took over five minutes! I would tweak the template and then rerun the builder and wait another five
minutes before I could see how it was rendered. Five minutes is far too long for a feed- back loop to be productive.

I recognized that these tools didn’t fix the maintenance issues I experienced with WordPress; they just shifted it to the dev machine. I thought it must be possible to write a better and simpler static site generator and was looking for a project to learn Go anyway. I spent the next couple of days writing a small prototype. The prototype confirmed that a website engine in Go could be magnitudes faster than the existing ones, and it would fix my installation experience as well. I spent the next few months designing and writing Hugo, incorporating my 20 years of experience working with and building CMSs and taking inspiration from everywhere.

I ported my blog to Hugo and announced my first Go project to the world in July 2013. At the time, I had no idea how this personal project, which I simply wrote for my own blog, would change my life and change the world. To build Hugo the way I wanted to design it forced me to invent new libraries in Go, several of which (notably Cobra, Viper, and Afero) have gone on to be some of the most popular in Go’s ecosys- tem, with adoption from Kubernetes, Docker, GitHub, and thousands of others. The experience of writing Hugo ultimately led me to join the Go team as the product lead in 2016 to help shape the future of the language.

Hugo’s simple and accessible design, combined with its unparalleled performance and productivity, immediately gained attention. Hugo continued to grow in adoption and popularity, ultimately becoming the most popular static site generator and one of the most popular open source CMS systems. It’s currently rated as #13 based on a number of websites (https://trends.builtwith.com/cms/open-source). Along with this growth came a small but dedicated contributor base, including Bjørn Erik Pedersen who succeeded me as the lead developer of Hugo.

Hugo also attracted the attention of Atishay Jain, an innovative software engineer who had a part in developing many of Adobe’s technologies that we’re all familiar with. He’s written this book, Hugo in Action, which is straightforward and approach- able. It explains not only how to use Hugo but also explains the history of how things came to be and the context of each decision you make through the process.

Beginners will deeply appreciate chapter 2’s “Live in 30 minutes” section, which provides plenty of guidance to make even people who are new to command-line appli- cations and websites feel comfortable. All readers will benefit from the breadth and context that this book provides. I personally appreciated chapter 9’s recipes to extend Hugo using external APIs, which expand the functionality of Hugo  to  include  dynamic features while retaining Hugo’s security and performance advantages.

—STEVE FRANCIA
creator of Hugo

# preface

The World Wide Web was initially a document delivery mechanism. Early web pages were documents that presented the same contents to everyone and were present as a file on disk. Early web browsers were more like a printer that would deliver the docu- ments on the screen. The significant achievement of the web was document delivery from a server far away, managed by someone else, and the ability to navigate across documents via hyperlinks. Developers always wanted to do more. They wrote scripts to generate all combinations of web pages to make the system appear dynamic. As the number of combinations increased, we found that we could support an infinite num- ber of variations by dynamically generating the web pages on a server. This approach brought a lot of complexity that the mainstream web community has been dealing with ever since.

My first website had a total of 10 pages. It lasted on the internet for eight months. When it was defaced the first time, I tried to set it up again. But I had neither the skills nor the perseverance to keep it running for a long time. This whack-a-mole game con- tinued across multiple technology stacks, frameworks, and approaches. Either pay someone to keep your system secure or dedicate yourself to keeping it up. The cycle of redoing the website continued until I landed on the Jamstack. Very few websites need infinite combinations of pages. For the rest, the run-time content generation approach is suboptimal both from the maintenance and performance perspectives. The Jamstack is a flashback to the generate-all-combinations era with just one catch—we can still do infinite combinations using JavaScript for the cases where there is a need. For the sig- nificant portions of most websites, we can be free of all the complexity.

When I first picked up Hugo, I didn’t realize how much of it was unlearning the web development conventions used in the run-time development model. Although images should always get stored with the rest of the document, static and dynamic content constraints forced this to be different. The more I used Hugo, the more I found about its way of doing things. The lack of structured learning resources caused a lot of rework. That is what triggered me to write this book. Hugo is an engineered product, not a mashup of multiple technologies to catch up to the trends or a solution covering years of cruft under a set of buzzwords. Hugo deserves a proper learning resource that presents the most straightforward web development approach and showcases how we can use Hugo to do much more than what it humbly advertises. That is what this book is about—setting up for simplicity and success.

As I wrote this book, my website has been sitting patiently. I do not have to spend a single second to maintain it. After a hiatus of two years, I can pick it up from where I left it, whenever I want, to make incremental improvements. This book is about fast websites that can last without continuous monitoring, unlike the approaches I tried in the past.

# acknowledgments

This is my first book, and I when I signed up for it, I had no idea what I was signing up for. What was planned as a six-month project took two years to complete, thanks to changing personal circumstances (arrival of kids) and changes all around the globe (the COVID-19 pandemic).

I would sincerely like to thank my wife, Ritika, who went through a tough preg- nancy, premature delivery, and a month-long stay in NICU—all while I was writing this book! Without her constant support and inspiration, this book would never have hap- pened. This book also required continuous support from my parents, work col- leagues, and friends who made time for me to get it done.

Next, I would like to thank my editor, Katie Sposato Johnson, for helping me comb through the entire set of guidelines to complete the book in the right format. She had answers with additional resources and guidelines for everything. I really appreciate the accommodation that the entire Manning team provided with my slippage of dead- lines again and again, specifically, Deirdre Hiam my project editor; Frances Buran, my copyeditor; and Keri Hales, my proofreader.

This book would not have been the same without the readers and reviewers on the livebook forums and the structured reviews. They, with their sharp critiques, changed the direction of the book multiple times. The first two chapters have been redone almost 20 times with major and minor tweaks based on places where the readers got stuck. It was great to see the roadblocks getting removed, albeit slowly, with each change as more and more readers could get through the initial hurdles and get into enjoying Hugo. To all the reviewers: Al Norman, Alberto Ciarlanti, Alex Lucas, Amit

Lamba, Anton Rich, Cena Mayo, Clive Harber, Darrin Bishop, David Jacobs, David Pardo, Guy Ndjeng, Hilde Van Gysel, Jeff Smith, Jerome Meyer, Joseph Houghes, Joshua White, Jürgen Hötzel, Lakshmi Narasimhan, Marjorie Roswell, Michael Bright, Milorad Imbra, Riccardo Marotti, Sander Zegveld, Sau Fai Fong, Taylor Dolezal, Theofanis Despoudis, and Vidhyadharan Deivamani, your suggestions helped make this a better book.

Of course, nothing was possible without @spf13, @bep, and the entire team that has made Hugo the ultimate static site builder. The thought and care that has gone into making Hugo is evidenced in the way its core structure and ideas have survived unchanged as the Jamstack concepts and services have matured. The Hugo commu- nity is a marvel, and it is a pleasure to have had healthy discussions on the Hugo forums for not only problems and solutions, but also for approaches, pros and cons, and performance considerations for doing things in a certain way.

Lastly, I would like to thank the service providers, GitHub, Netlify, Formspree, Stripe, and SendGrid, for having stable backbone services for us to be able to build upon. These services are affordable, reliable, and have allowed us to focus on what we love the most—creating new websites.

# about this book

Hugo in Action guides you through building a fast and low maintenance website using the Hugo static site builder. It enables you to understand the core concept of the Jam- stack and the profound impact of its compilation step on the website’s  architecture. This book provides a step-by-step walkthrough for laying out content, organizing tem- plates, and managing assets in a Hugo-based website. It provides the best practices for building a quick-to-compile, quick-to-load, and easy-to-maintain website, along with the means to debug issues, optimize existing template files, and set the website’s archi- tecture for optimal usage of Hugo.

## Who should read this book

Hugo is a tool for web developers looking for a powerful static site builder to create feature-rich websites without compromising run-time performance, developer experi- ence, and maintainability. This book expects its readers to understand HTML, CSS, JavaScript, and version control using Git and GitHub-based code hosting. The readers should also be familiar with the basic usage of the command line, including navigat-  ing through the filesystem and running simple commands. Both beginner and experi- enced web developers will benefit from this book.

## How this book is organized: A road map

The entire book runs through a single example website for a fictional company called Acme Corporation. We’ll build the site and add new features to improve its behavior while introducing approaches to development.

The book has two distinct parts. The first part focuses on the core functionality of Hugo, which we will run in isolation from the rest of the internet. The second part centers on how Hugo provides the means to communicate with various services and how the JavaScript ecosystem furnishes the functionality that is not possible during Hugo’s compilation step.

- Chapter 1 introduces the Jamstack and explains the ideas behind it. This chap- ter also lays out the parts of the Jamstack and how these work together. It also introduces the Hugo static site builder and discusses when it is sensible to use Hugo and when it is inappropriate to use Hugo or the Jamstack.
- Chapter 2 provides a brief overview of a Hugo project’s working directory. It also sets up web hosting and creates a simple Hugo-based website that is live on the internet, which offers outstanding performance and a manageable set of dependencies.
- Chapter 3 lets us play the role of the content author. This chapter provides an in-depth overview of Markdown and YAML, the two main languages used to cre- ate content and provide metadata for a Hugo website. It also compares these languages with other available options and provides an overview of the standard metadata properties we can use in the front matter of a Hugo web page.
- Chapter 4 allows us to play the role of the website editor. This chapter shows how to organize pages in a Hugo website into sections, menus, and Hugo taxon- omies, how to bunch contents into a page bundle, and how to effectively use Hugo’s built-in and community-provided shortcodes to enable and extend Markdown features.
- Chapter 5 offers our first glimpse of the Go template language that provides the means to control the rendering of a web page. We will explore how to build cus- tom pages in Hugo, how to render content with the Go template language, how to access Hugo’s variables, functions, configurations, and front matter, and how to read from the filesystem using Hugo.
- Chapter 6 explores the critical components of a Hugo theme and the tools Hugo provides for building custom web pages. It teaches us how to organize templates for easy maintenance and reuse, to improve productivity by sharing template code and snippets between multiple page types, and to tackle resource management issues with Hugo pipes.
- Chapter 7 allows us to take full ownership of the website. It shows how the building blocks of Hugo’s content system (the leaf and branch bundles, the tax- onomy system, layouts, and types) all map to template code.
- Chapter 8 dives deep into Hugo Modules, which are a powerful, widely misun- derstood, and underused feature of Hugo. Hugo’s modules allow the creation and consumption of plugins (from themes and templates to shortcodes and even content) from all the components of a Hugo-based website.
- Chapter 9 steps outside of the bounds of our project folder and  showcases Hugo’s support for the second pillar of the Jamstack—APIs. This chapter moves us into Web 2.0 with support for dynamic features like comments and contact forms. It also presents some simple solutions to historically more challenging problems such as dynamic surveys and RESTful GET APIs.
- Chapter 10 shows why Hugo goes to great lengths to ensure that it plays nicely with JavaScript (the “J” in Jamstack). This includes customizing and integrating with one of the fastest JavaScript bundlers. Hugo clarifies concerns between the compile-time and run-time environments while still keeping tight integration and providing unified control. This chapter uses client-side scripting for dynamic features like background form submissions and the npm ecosystems for client-side searches. It also sets up a hybrid website with Hugo and JavaScript that takes ownership of the pieces they excel in.
- Chapter 11 introduces the Jamstack way of building low-maintenance APIs to extend Hugo with features that it does not natively provide. We do this without losing the key performance benefits of Hugo. This chapter also explores web- hooks—the server-to-server API communication mechanism that integrates with independent API providers—to enable our website to act as a unified back- end with little operational overhead.
- Chapter 12 dives into a capstone project where everything from the book is put into practice. This chapter busts some of the most popular myths of the Jam- stack by building an e-commerce website with end-to-end support from the shopping cart to checkout to order fulfillment.
- Chapter 13 takes the existing website and stretches it in multiple directions. This provides support for numerous (human) languages and many views of the same content with different themes. It also makes our website even faster with offline support, instant pages, and Turbo techniques and libraries. It also dis- cusses scripting to reduce the work done manually in the browser and participa- tion in the Hugo community for support, appreciation, and contribution.

The chapters in this book should be read in order: what you learn from previous chap- ters is built upon in the following ones. Each chapter improves the example website from where it was left in the last chapter. If the reader, by chance, wants to understand a topic out of order, it is advised to look at the code checkpoint at the end of the pre- vious chapter to understand where the next chapter starts.

## About the code

This book contains many examples of source code, both in numbered listings and in line with normal text. In both cases, the source code is formatted in a fixed-width font like this to separate it from ordinary text.

In many cases, the original source code has been reformatted; we’ve added line breaks and reworked indentation to accommodate the available page space in the book. In rare cases, even this was not enough, and listings include line-continuation
markers (➥). Additionally, comments in the source code have often been removed from the listings when the code is described in the text. Code annotations accompany many of the listings, highlighting important concepts.

The book has over 128 code checkpoints and more than 94 chapter resources pres- ent on GitHub with links to the exact checkpoint associated with any section immedi- ately after the section. You can get executable snippets of code from the liveBook (online) version of this book at https://livebook.manning.com/book/hugo-in-action. The complete code for the examples in the book is available for download from the Manning   website   at   https://www.manning.com/books/hugo-in-action,   and   from GitHub at https://github.com/hugoinaction/hugoinaction.

The resources provide easy-to-use copies of the code samples embedded through- out the book and assets like CSS files and the images used to build the example web- site. Code checkpoints provide working code up to the point in the book where it is referenced and are presented as branches in the GitHub repository. We can compare two checkpoints between any sections in the text to see the changes between those two sections.   For   example,   https://github.com/hugoinaction/hugoinaction/compare/ chapter-03-06...chapter-04-11 provides all the changes as commits messages between code checkpoints chapter-03-6 and chapter-04-11. It also provides a diff between the two checkpoints. Each checkpoint can also be viewed live on the book’s website in a subdomain like https://chapter-04-11.hugoinaction.com, which offers a working ver- sion of the website at chapter 04, checkpoint 11. The readme file for the repository also provides summaries and links to additional chapter resources and checkpoints. You can clone the code repository locally and use git checkout <checkpoin or chap- ter resource name> to get to a specific code checkpoint or to a specific chapter’s resources.

TIP Code checkpoints are a vital tool in debugging issues. Some details with light documentation can be gleaned from code checkpoints. Readers can compare their code to a checkpoint to figure out and fix misunderstandings and mistakes.

## liveBook discussion forum

Purchase of Hugo in Action includes free access to liveBook, Manning’s online reading platform. Using liveBook’s exclusive discussion features, you can attach comments to the book globally or to specific sections or paragraphs. It’s a snap to make notes for yourself, ask and answer technical questions, and receive help from the author and other users. To access the forum, go to https://livebook.manning.com/book/hugo-in- action/discussion. You can also learn more about Manning's forums and the rules of conduct at https://livebook.manning.com/discussion.

Manning’s commitment to our readers is to provide a venue where a meaningful dialogue between individual readers and between readers and the author can take place. It is not a commitment to any specific amount of participation on the part of the author, whose contribution to the forum remains voluntary (and unpaid). We suggest
you try asking the author some challenging questions lest his interest stray! The forum and the archives of previous discussions will be accessible from the publisher’s website as long as the book is in print.

## Other online resources

The official documentation website for Hugo is https://gohugo.io/documentation/. It provides a complete list of all available Hugo parameters and features. The Hugo community at https://discourse.gohugo.io/ can be of immense help in figuring out best practices, asking for help, or providing feedback.

# about the author

ATISHAY JAIN is a senior computer scientist at Adobe. He is an experi- enced web developer, developing web-based software used by mil- lions of Adobe Creative Cloud customers on a daily basis and has contributed to many Adobe tools, including Photoshop, Acrobat and Illustrator. Atishay is a guest author at CSS-Tricks and is a regu- lar conference speaker at web conferences. He has his own personal
website with a 100/100 score on Google Lighthouse, focusing on the performance of all the features of a regular website. Learn more about Atishay at https://atishay.me.

# about the cover illustration

The figure on the cover of Hugo in Action, “Femme de cracovie,” or “A Woman from Krakow,” is taken from a collection by Jacques Grasset de Saint-Sauveur, published in 1797. Each illustration is finely drawn and colored by hand.

In those days, it was easy to identify where people lived and what their trade or sta- tion in life was just by their dress. Manning celebrates the inventiveness and initiative of today’s computer business with book covers based on the rich diversity of regional cul- ture centuries ago, brought back to life by pictures from collections such as this one.

