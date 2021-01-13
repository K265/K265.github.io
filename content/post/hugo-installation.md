---
title: "Hugo Installation"
date: 2021-01-13T10:59:25+08:00
draft: false
summary: Create a Hugo site using the beautiful GitHub style theme.
tags: ["Hugo"]
---

# Hugo Installation

<https://github.com/gohugoio/hugo>

<https://gohugo.io/getting-started/quick-start/>

<https://github.com/MeiK2333/github-style>

```shell
hugo new site blog
cd blog
git init
git submodule add https://github.com/MeiK2333/github-style.git themes/github-style
## under git bash
echo 'theme = "github-style"' >> config.toml
hugo new post/hugo-installation.md
hugo server -D
```

