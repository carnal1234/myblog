---
title: IIFE
date: 2023-10-18
tags:
  - Javascript
categories: Javascript
---

## **What is IIFE**

IIFE is a function that is defined and executed immediately in the same line of code. 

The main purpose of an IIFE is to create new scope in your code, which can help to avoid naming conflicts and keep your code more organized.


One of the main benefit of IIFE is to avoid global namespace pollution. We can take a look into the following function


Before we talk about IIFE, let us look into function in JS.


```js
var name = "Brian";
//Function declaration
function logger() {
 console.log(name);           // logs Brian
 console.log(window.name);    // logs Brian
}
window.name = "John"
logger(); //John
---------------
//Function Expression
(function () {
  var loc = "Brian";
function logger() {
 console.log(name);         // logs Brian
 console.log(window.name);  // logs undefined
}
logger(); //Brian
}) ()
```

In the above example, variable ```loc``` is accessible through ```window```, which is a global variable. This is not ideal because we don't want variable to be accessed by everyone.

One way to avoid this is using IIFE. The second example localize the variable within the scope. So you can't access from outside.

Beside localizing the variable, you can open access point by returning inside IIFE. 

Take a look into the following code
```js
let api = (function(){
  let data = 1;
  
  init = function(){
    console.log("init");
  }
  
  getData = function(){
    return data;
  }

  setData = function(x){
    data = x;
  }
  
  
  return {init : init, getData: getData, setData: setData};
})()

console.log(data) //error
console.log(api) //{init: ƒ, getData: ƒ, setData: ƒ}

api.data = 10; //error

```

It is a simple api function which return getter and setter.

```data``` can only be accessed by ```getData``` and modified by ```setData``` function. 

In other words, inner variable is protected and can be interacted by exposing some function to outside. It is exactly what api does. 



## Conclusion

IIFE is a conventient way to localize your variable inside the same scope. It avoid variable from being accessed outside and is a good practice to build and organize the code. Whether you’re building small scripts or large-scale applications, understanding and using IIFE effectively can significantly improve code maintainability and reliability. That it for today. Thank you.


For more detail, you can read the following article. 

<a>[Essential JavaScript: Mastering Immediately-invoked Function Expressions](https://medium.com/@vvkchandra/essential-javascript-mastering-immediately-invoked-function-expressions-67791338ddc6)</a>



