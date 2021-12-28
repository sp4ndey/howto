---
title: "Run psql in a Docker Container"
date: 2021-06-14T10:38:42-07:00
draft: false
tags:
- docker
- postgres
---
This is convenient if I already have Docker installed on the machine, but not Postgres, and I need to connect to a remote Postgres server.

```bash
docker run -it --rm postgres psql "postgresql://username:password@host/database"
```

[source](https://hub.docker.com/_/postgres)
