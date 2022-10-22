---
weight: 6
title: "8.6 Viewing the dependencies source code"
date: 2022-09-12T18:26:30+08:00
draft: true
---

# 8.6 Viewing the dependencies source code

By moving to Hugo Modules, we lost the ability to inspect the source code of the dependencies. Also, because dependencies are not a part of the website’s source code, our website will need internet access to be compiled. 

Internet dependency may turn out to be a limitation in certain use cases. If we archive our website for long-term storage, backing up a copy of the dependencies is as important as backing up the source code.

To perform this task, we can run hugo mod vendor. Hugo creates a folder called vendor with the source code of all the dependencies. Not only that, if this folder is present and contains the dependencies, Hugo does not go to the internet to build our website. We can check in this folder, just like the resources folder, with our source code.

{{< hint info >}}
**Why not vendor by default?**

Hugo’s decision not to have the vendor folder present by default provides better efficiency. Hugo can download it only once and share it across multiple projects if two projects use the same module. Also, keeping the dependencies hidden ensures that we follow the development practices of not modifying the dependencies and getting the changes done through official means (updating the dependency version). In-place hot patches in dependencies have a high possibility of being missed in a commit to source control, leading to broken builds.
{{< /hint >}}

{{< hint info >}}
**CODE CHECKPOINT**    https://chapter-08-04.hugoinaction.com, and source code: https://github.com/hugoinaction/hugoinaction/tree/chapter-08-04.
{{< /hint >}}