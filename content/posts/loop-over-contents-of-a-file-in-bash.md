---
title: "Loop over contents of a file in Bash"
date: 2024-04-22T08:54:57-07:00
draft: false
tags:
- bash
- zsh
---

To iterate over every line in a file, we need to use a while loop, instead of [for loop](/posts/write-a-for-loop-in-bash/).

```shell
while IFS= read -r line; do echo "$line"; done < /path/to/file
```

[source](https://stackoverflow.com/a/30735977)
