---
title: "Check if a JSON array in PostgreSQL contains a value"
date: 2025-01-29T23:10:19-08:00
draft: false
tags:
- postgres
---

Say you have a table named `books`, with a JSON column, `metadata`, and within this column, there is an array named `tags`.

The data in this table might look like this:

|      title       |               metadata                |
|------------------|---------------------------------------|
| Ready Player One | {"tags": ["sci-fi", "gaming"]}        |
| Snow Crash       | {"tags": ["sci-fi", "cyberpunk"]}     |
| In Real Life     | {"tags": ["graphic novel", "gaming"]} |

Now, say you want to find out all the books that have the tag `gaming`. You can extract the `tags` field using the `->` operator, and check whether or not it contains `gaming` using the `?` operator.

```sql
SELECT title, metadata FROM books WHERE metadata->'tags' ? 'gaming';
```

which will return:

|      title       |               metadata                |
|------------------|---------------------------------------|
| Ready Player One | {"tags": ["sci-fi", "gaming"]}        |
| In Real Life     | {"tags": ["graphic novel", "gaming"]} |

[source](https://www.postgresql.org/docs/current/functions-json.html)
