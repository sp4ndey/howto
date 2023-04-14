---
title: "Run Hugo server locally"
date: 2023-04-14T13:36:11-07:00
draft: false
tags:
- hugo
---

This website is built using [Hugo](https://gohugo.io/). I use [git submodules](https://git-scm.com/book/en/v2/Git-Tools-Submodules) to add the theme, so when I want to run the website locally, there is one additional command needed to pull in the files for the theme:

```shell
git submodule update --init
```

After this, simply run:

```shell
hugo server
```

That's it!

More details of the `hugo server` command can be found [here](https://gohugo.io/commands/hugo_server/).
