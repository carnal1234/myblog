
#What is IIFE



Important Link Below

<a>[Essential JavaScript: Mastering Immediately-invoked Function Expressions](https://medium.com/@vvkchandra/essential-javascript-mastering-immediately-invoked-function-expressions-67791338ddc6)</a>


Before we talk about IIFE, let us look into function in JS.


```js
var msg = "Hello World";

//normal function
function traditionFunc(){
  console.log(msg);
}

//Anonymous function expressions
let AnonymousFunc = function(){
  console.log(msg);
}

let NamedFunc = function func(){
  //do something
}

traditionFunc(); //Hello World
AnonymousFunc(); //Hello World

```

In the above example, Both function produce same result and log message to console.

<h4>Anonymous function expressions</h4>

















IIFE (Immediately Invoked Function Expression)

is a way to avoid inner variable go outside



```js
let api = (function(){
  let data = 1;
  
  init = function(){
    console.log("init");
    run();
  }
  
  run = function(){
    console.log("running");
  }
  
  
  return {init : init};
})()

```

Now only init function is exposed to user.

We cannot modify the data inside IIFE.

And you can choose what method to be exposed by api in return.



