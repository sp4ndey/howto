---
title: "Write a file to S3 in Node.js"
date: 2022-01-07T16:10:32-08:00
draft: false
tags:
- aws
- javascript
- s3
---

Once I had figured out how to [read a file from S3](../read-a-file-line-by-line-from-s3-in-node.js/), I then had to write one. Given that the text I had to write wasn't large, this turned out to be very straightforward. Tested with [AWS SDK](https://aws.amazon.com/sdk-for-javascript/) v3.45.

```javascript
const AWS = require("@aws-sdk/client-s3");

const writeFile = async (bucket, filename, text) => {
    const s3 = new AWS.S3();

    await s3.putObject({
        Bucket: bucket,
        Key: filename,
        Body: Buffer.from(text)
    })
}
```

see also: [Read a file line by line from S3 in Node.js](../read-a-file-line-by-line-from-s3-in-node.js/)
