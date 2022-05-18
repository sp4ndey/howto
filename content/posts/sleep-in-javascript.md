---
title: "Sleep in Javascript"
date: 2022-05-18T14:44:56-07:00
draft: false
tags:
- javascript
- typescript
---
Recently, I was writing a script in TypeScript where I was calling an API a few hundreds of times. I wanted a brief delay between the API calls, when I found out that there is no built-in `sleep` in Javascript.

Fortunately, it was easy enough to implement:
```typescript
export const sleep = (ms: number) => new Promise(resolve => setTimeout(resolve, ms));
```

Sample usage:
```typescript
for (const item of items) {
    // TODO: do some work

    // wait for 100ms
    await sleep(100);
}
```

[source](https://stackoverflow.com/a/39914235)
