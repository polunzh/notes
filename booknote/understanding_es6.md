## Promose

### Promise 链的返回值问题

Promise 链的另一个重要特性是可以给下游 Promise 传递数据。

``` javascript
let p1 = new Promise(function(resolve, reject) {
    resolve(42);
});

p1.then({
    console.log(value);    // "42"
    return value + 1;
}).then(function(value){
    console.log(value);	   // "43"
});
```

### Promise 链中返回 Promise

``` javascript
let p1 = new Promise((resolve, reject) => {
    resolve(42);
});

let p2 = new Promise((resolve, reject) => {
    resolve(43);
});

p1.then(value => {
    console.log(value);    // "42"
    return p2;
}).then(value => {
    console.log(value);    // "43"
});
```

