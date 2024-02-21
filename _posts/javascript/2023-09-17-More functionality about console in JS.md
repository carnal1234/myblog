---
title: Console in JS
date: 2023-09-17
tags:
  - Javascript
categories: Javascript
---

## **Console in Javascript**

In Javascript, we often use console to log object. But there is much more functionality about console.
 
Instead of logging each object, we can group multiple object in one. 
And object would use its variable name as key. 

We can even log array in a table by ```console.table```

```js
let john = {name: "john", age: 16, job: "student"}
let mary = {name: "mary", age: 31, job: "teacher"}
let tom = {name: "tom", age: 42, job: "engineer"}

console.log({john, mary, tom}); //Log object together with name

console.table([john, mary, tom]); //Log object as table

```
## Logging Time

In some cases, we want to know the time required between a function, 
we could use ```console.time``` and ```console.timeEnd``` with same name, then browser would output time in millisecond.



```js
function looping(){
  let i = 0;
  while(i < 1000000){
    i++;
  }
}

console.time("timer");
looping();
console.timeEnd("timer"); //Output -> timer: 2.074951171875 ms

```

## Stack Tracing

In Javascript, we could use ```console.trace``` to print the stack trace of all function call . The stack trace will be printed in the console.

It is useful especially with nested callback where it become difficult to pinpoint exactly the error coming from. 


```js
let foo = () => console.trace('foo');

foo();
```

## How to avoid console everywhere???



As a website developer, we often use console for debugging. However, it would be a messy ending up multiple console spread in different part of the code. Sometimes you may forget to delete the console and output unnecessary data to the browser.

To handle the issues, we could use a global boolean variable ```debugMessage``` and a custom ```log``` function as an wrapper of console. Here, different developers could use the same tool for debugging without worring about messy up the code.


```js
// Used for debug messages
  debugMessages = true;
    function log(log, level = 'l', ...args) {
        if (!debugMessages) return;

        const prefix = 'Remove Adblock Thing:'
        const message = `${prefix} ${log}`;
        switch (level) {
            case 'e':
            case 'err':
            case 'error':
                console.error(message, ...args);
                break;
            case 'l':
            case 'log':
                console.log(message, ...args);
                break;
            case 'w':
            case 'warn':
            case 'warning':
                console.warn(message, ...args);
                break;
            case 'i':
            case 'info':
            default:
        console.info(message, ...args);
        break
    }
    }

```


## Conclusion

This article introduced you to the different types of console methods. You can use these methods in your debugging journey.

Some methods look simple, but they are very useful in finding the bugs in your code.

If something goes wrong in your code these methods give you the ability to find the solution to your problem.
