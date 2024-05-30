---
title: "Group by Time in SQL"
date: 2024-05-29T21:29:11-07:00
draft: false
tags:
- postgres
- snowflake
---

Say you have a timestamp column, and you want to find out how many records are there for a particular day, or hour, or week. You can do this using the [date_trunc](https://www.postgresql.org/docs/current/functions-datetime.html#FUNCTIONS-DATETIME-TRUNC) function.

```sql
SELECT DATE_TRUNC('DAY', created_at), COUNT(*)
FROM my_table
GROUP BY DATE_TRUNC('DAY', created_at);
```

[date_trunc](https://docs.snowflake.com/en/sql-reference/functions/date_trunc) is also available in Snowflake.
