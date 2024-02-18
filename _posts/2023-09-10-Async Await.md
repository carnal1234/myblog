---
title: Async Await
date: 2023-09-10
tags:
  - Javascript
---
Async Await


In Js, we have promise that used in callback.

Promise is a micro task that



Async function automatically resolve the returned value as Promise


```js
let getUser = async(name) => {

  let users = {
    Mary: 'Teacher',
    John: 'Student',
    Brian: 'Developer'
  }
  return users[name];
}
```

This is the same as function below

```js
let getUser = (name) => {

  let users = {
    Mary: 'Teacher',
    John: 'Student',
    Brian: 'Developer'
  }
  return Promise.resolve(users[name]);
}

```
Async is useful when combined with Await

Note about Async

- only be used in async function
- used to wait for a Promise
- pause until a Promise is settled


Now let see how to use await + async

```js
//Async + Await

let makeSmooth = async() => {
  let a = await getUser('Brian');
  let b = await getUser('Mary');
  
  return [a, b];
}

```
notice that b run after a finishes.

So the code does not run concurrently

And we can do that in following

```js
let makeSmoother = async() => {
  let a = getUser('Brian');
  let b = getUser('Mary');
  
  return Promise.all([a, b]);
}

```

Assume getUser takes 1 second delay

makeSmooth takes 2 seconds as it wait the first one completed to execute next

makeSmoother takes 1 seconds only because it run concurrently

Therefore, await is a blocking code and must be used carefully











