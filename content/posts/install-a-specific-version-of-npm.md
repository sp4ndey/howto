---
title: "Install a specific version of NPM"
date: 2023-04-12T10:58:05-07:00
draft: false
tags:
- javascript
- nodejs
---

I use [nvm](https://nvm.sh) to manage [Node.js](https://nodejs.org/en) versions on my computer and I typically install the latest version of [npm](https://docs.npmjs.com/cli) that is compatible with the Node.js version. This is as simple as:

```shell
$ nvm install --lts --latest-npm
Installing latest LTS version.
...
Now using node v18.15.0 (npm v9.5.0)
Attempting to upgrade to the latest working version of npm...
...
* npm upgraded to: v9.6.4

$ node -v
v18.15.0

$ npm -v
9.6.4
```

or to install a specific version:

```shell
$ nvm install 16.20.0 --latest-npm
Downloading and installing node v16.20.0...
...
Now using node v16.20.0 (npm v8.19.4)

$ node -v
v16.20.0

$ npm -v
8.19.4
```

But sometimes a project requires a specific version of npm. This can be done using:

```shell
npm install -g npm@version
```

Continuing from our earlier example:

```shell
$ nvm use 16.20.0                 
Now using node v16.20.0 (npm v8.19.4)

$ node -v
v16.20.0

$ npm -v
8.19.4

$ npm install -g npm@8.12.0
...

$ npm -v
8.12.0
```

Note that this doesn't impact other node versions:

```shell
$ nvm use 18.15
Now using node v18.15.0 (npm v9.6.4)

$ nvm use 16.20
Now using node v16.20.0 (npm v8.12.0)
```
