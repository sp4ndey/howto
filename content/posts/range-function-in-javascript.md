---
title: "Range function in JavaScript"
date: 2021-12-31T13:38:42-08:00
draft: false
tags:
- javascript
---
JavaScript doesn't have a built-in equivalent of Python's [range](https://docs.python.org/3/library/functions.html#func-range) function. Although a _for_ loop isn't difficult to write, I occasionally miss the convenience of _range_.

The popular [lodash](https://lodash.com/) library includes a [range](https://lodash.com/docs/#range) function, but it's also easy enough to implement yourself without any additional libraries.

The most compact way to generate the range [0..n) is:
```javascript
[...Array(n).keys()]
```

Example:
```javascript
for (const n of [...Array(3).keys()]) {
    console.log(n);
}

/*
Output:
0
1
2
*/
```

This can also be written using [Array.from()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/from), which can be useful sometimes:
```javascript
Array.from({ length: n }, (_, i) => i)
```

Example:
```javascript
Array.from({ length: 3 }, (_, i) => {
    console.log(i);
})

/*
Output:
0
1
2
*/
```

A more elaborate implementation may look like:
```javascript
const range = (start, stop, step = 1) => {
    if (start == null) {
        throw 'range requires at least 1 parameter';
    }

    if (stop == null) {
        [start, stop] = [0, start];
    }

    const size = Math.floor((stop - start) / step);
    return Array.from({ length: size }, (_, i) => start + i * step);
}
```

Example:
```javascript
console.log(range(6));
// Output: [ 0, 1, 2, 3, 4, 5 ]

console.log(range(4, 10));
// Output: [ 4, 5, 6, 7, 8, 9 ]

console.log(range(17, 28, 2));
// Output: [ 17, 19, 21, 23, 25 ]
```

[source](https://stackoverflow.com/questions/3895478/does-javascript-have-a-method-like-range-to-generate-a-range-within-the-supp)
