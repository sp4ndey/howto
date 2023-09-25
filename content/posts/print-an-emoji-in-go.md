---
title: "Print an Emoji in Go"
date: 2023-09-24T19:55:44-07:00
draft: false
tags:
- go
---

When writing debug messages to logs or console, I find it useful to use emojis to bring attention to certain lines. In Go, you can do this in two ways -

Add emojis directly in the code:
```go
println("🚨 🚨 🚨 ATTENION! 🚨 🚨 🚨")
```

Or use the Unicode code point:
```go
println("\U0001F6A8 \U0001F6A8 \U0001F6A8 ATTENION! \U0001F6A8 \U0001F6A8 \U0001F6A8")
```

In both cases, the output will look like this:
```
🚨 🚨 🚨 ATTENION! 🚨 🚨 🚨
```
