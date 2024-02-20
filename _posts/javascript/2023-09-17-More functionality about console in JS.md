---
title: Console in JS
date: 2023-09-17
tags:
  - Javascript
categories: Javascript
---


How to log multiple obj??

```js
let john = {name: "john", age: 16, job: "student"}
let mary = {name: "mary", age: 31, job: "teacher"}
let tom = {name: "tom", age: 42, job: "engineer"}

console.log({john, mary, tom});

console.table([john, mary, tom]);

```

How long the function run??


```js
function looping(){
  let i = 0;
  while(i < 1000000){
    i++;
  }
}

console.time("timer");
looping();
console.timeEnd("timer");
```


How to trace function??

```js
let foo = () => console.trace('foo');

foo();
```
