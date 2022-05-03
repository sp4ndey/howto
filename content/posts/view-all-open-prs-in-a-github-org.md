---
title: "View all open PRs in a Github Organization"
date: 2022-05-03T09:28:21-07:00
draft: false
tags:
- github
---
If your organization has multiple repositories, it may be useful to view all open PRs across all of them, even if you have not been requested to review them. This is as simple as going to:
```
https://github.com/pulls?q=is%3Apr+is%3Aopen+user%3A{YOUR_ORGANIZATION_NAME}
```

Example: https://github.com/pulls?q=is%3Apr+is%3Aopen+user%3Apython

