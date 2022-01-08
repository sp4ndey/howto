---
title: "Read a file line by line from S3 in Node.js"
date: 2022-01-07T15:41:11-08:00
draft: false
tags:
- aws
- javascript
- s3
---

I had to do this recently, and it's actually quite straightforward... once you know what to do.

One problem I faced was that all the blogs and [Stack Overflow](https://stackoverflow.com/) answers I found were about the [AWS SDK](https://aws.amazon.com/sdk-for-javascript/) v2 and they don't work with v3. The following code has been tested with AWS SDK v3.45.

```javascript
const AWS = require("@aws-sdk/client-s3");
const readline = require("readline");

const readFile = async (bucket, filename) => {
    const s3 = new AWS.S3();

    const file = await s3.getObject({
        Bucket: bucket,
        Key: filename
    });

    const reader = readline.createInterface({ input: file.Body });

    for await (const line of reader) {
        // process each line
    }
}
```

see also: [Write a file to S3 in Node.js](../write-a-file-to-s3-in-node.js/)
