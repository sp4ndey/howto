---
title: "Rebase the First Commit in a Git Repository"
date: 2022-01-03T12:40:43-08:00
draft: false
tags:
- git
---

The `--root` option of `git rebase` allows you to rebase the first commit in a repository. This is useful sometimes when setting up a new repository, which is not very often, but still...

```shell
git rebase -i --root
```

[source](https://stackoverflow.com/a/23000315/4170899)
