---
weight: 1
title: "8.1 Setting up Hugo Modules"
date: 2022-09-12T18:26:30+08:00
draft: true
---

# 8.1 Setting up Hugo Modules

Hugo Modules have a dependency on Go. You can install Go using your package man- ager or using the instructions at https://golang.org/doc/install. Remember that Go needs to be present in the system path to be usable by Hugo.

To verify if Go is available, run the command go version, which outputs the version of Go in the console. Ensure that the version of Go is greater than 1.12. Once we have a supported version of Go installed, we can forget about Go and get back to Hugo. This installation is all that we will deal with in the Go language for the entire book.

{{< hint info >}}
**NOTE** Having Go installed is essential to complete the exercises in the rest of the book. We will use Hugo Modules in the second half of the book.
{{< /hint >}}

The next step is to initialize Hugo Modules. Each Hugo module needs a module name. This name identifies the module. The module name is used only in the context of Hugo Modules. To initialize a module named AcmeCorporationWebsite, on the command line, run the command in the following listing.

{{< details title="Listing 8.1  Hugo command to create a new module" open=true >}}
```
hugo mod init AcmeCorporationWebsite
```
{{< /details >}}

This command creates a file called go.mod in the root folder. Each module has a go.mod file. This file is the entry point for Hugo Modules. It identifies the current module and stores the information about the other modules that this module links to. This file is similar in concept to Gemfile in Ruby, package.json in Node.js, and requirements.txt in Python’s pip. It lists the dependencies and their versions that we can use during installation and update. We can use this file to scan the list of direct dependencies. We should check this file into version control, and in most cases in the Hugo world, we do not modify it manually.

{{< hint info >}}
**Exercise 8.1**

True or False: If we are developing a single website, there are no advantages to Hugo Modules.
{{< /hint >}}

{{< hint info >}}
**Why go.mod when we have config.yaml**

Hugo Modules is a unique feature in Hugo in many respects. Go needs to be installed, it has an extra initialization command, and a separate go.mod file. This sep- aration is necessary because Hugo Modules is a lightweight wrapper over Go mod- ules. If instead of hugo mod init you called go mod init, you would find that it behaves the same. Hugo chose the Go modules as the basis for its module system for a variety of reasons:
- It is a high performance, well maintained, highly flexible feature with sensible defaults. You can link to anything from an individual file in a server repository to a folder from another module.
- Hugo is built using Go. This does not add a new maintainability risk (remem- ber from section 2.5.2, every dependency can require additional mainte- nance) to the websites using Hugo.
- Writing and maintaining a module system that involves managing dependen- cies downloaded from the internet is hard. Apart from performance, security is a big concern. By wrapping Go modules, the Hugo team gets a powerful fea- ture at a low cost.
- The standard go.mod file has its advantages. Auditors inspecting Hugo web- sites need one file, and vulnerability detection systems are much more likely to support the Go language than the Hugo web development framework.

Hugo’s team has built some clever optimizations and tight integration into Hugo Mod- ules. Even if you are a Go developer familiar with Go modules, Hugo Modules pro- vides many great surprises. Hugo has personalized the Go modules by automatically filling go.mod with custom mappings for folder locations and with the ability to pick and choose plugin types. For Hugo developers, go.mod is a machine-generated file in most cases. Like the resources folder, go.mod does not need to be touched manu- ally; just check it in with the source code. Hugo can figure out the dependencies using the configuration and create go.mod files automatically.
{{< /hint >}}