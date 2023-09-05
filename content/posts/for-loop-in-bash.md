---
title: "Write a for loop in Bash"
date: 2023-09-05T11:02:44-07:00
draft: false
tags:
- bash
- zsh
---
Occasionally I need to run the same shell command or set of commands in a loop. The one-liner syntax for doing this in bash or zsh is:

```shell
for i in {1..10}; do echo $i; done
```

Multiple commands can be run:

```shell
for i in {1..10}; do echo "$i*2"; echo $((i*2)); echo "----"; done
```

And a step value can also be given:

```shell
for i in {1..10..2}; do echo $i; done
```
