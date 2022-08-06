---
title: "Search Git History for a string"
date: 2022-08-05T11:30:29-07:00
draft: false
tags:
- git
---
Occasionally, when looking at a block of code, I want to find out which commit first introduced a particular word. It could be a function name or a variable name. Or which commit took it out. In [Mercurial](https://www.mercurial-scm.org/), I used to use `hg grep` for this. Fortunately, this is easy to do in `git` as well.

```shell
git log -S <search string> --source --all
```

[source](https://stackoverflow.com/a/5816177)
