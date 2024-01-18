---
title: "Calculate the duration between two timestamps in PostgreSQL"
date: 2024-01-17T10:12:38-08:00
draft: false
tags:
- postgres
---

Say you have a table with two `timestamp` columns and want to calculate the duration between them. Subtracting one `timestamp` from another returns an `interval`. You can then convert this interval to a number of seconds using `EXTRACT(EPOCH FROM ...)`.

```sql
SELECT created_at, updated_at, EXTRACT(EPOCH FROM (updated_at - created_at)) AS duration FROM my_table
```

[source](https://www.postgresql.org/docs/current/functions-datetime.html#FUNCTIONS-DATETIME-EXTRACT)
