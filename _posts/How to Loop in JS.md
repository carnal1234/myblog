

```js
const orders = [500, 30, 99, 15, 223];


'Bad Loop Code 💩'

const total = 0;
const withTax = [];
const highValue = [];
for (i = 0; i < orders.length; i++) { 

    // Reduce
    total += orders[i];

    // Map
    withTax.push(orders[i] * 1.1);

    // Filter
    if (orders[i] > 100) {
        highValue.push(orders[i])
    }
}


'Good Loop Code ✅'

// Reduce
const total = orders.reduce((acc, cur) => acc + cur)

// Map
const withTax = orders.map(v => v * 1.1)

// Filter
const highValue = orders.filter(v => v > 100);

/**
 * Every
 * @returns false
 */
const everyValueGreaterThan50 = orders.every(v => v > 50)

/**
 * Every
 * @returns true
 */
const everyValueGreaterThan10 = orders.every(v => v > 10)


/**
 * Some
 * @returns false
 */
const someValueGreaterThan500 = orders.some(v => v > 500)

/**
 * Some
 * @returns true
 */
const someValueGreaterThan10 = orders.some(v => v > 10)
```


---
Iterator


iterator is used to customize the behaviour of for of loop


```js
const arr = ["teacher", "student", "engineer"];



//Simplest Way to Loop

for(let i = 0; i < arr.length; ++i){
  console.log(arr[i]);
}



//For of loop

for(const e of arr){
  console.log(e);
}


arr[Symbol.iterator] = function(){
  let i = 0;
  let arr = this;
  return {
    next: function(){
      if(i >= arr.length){
        return {done: true};
      }else{
        const value = arr[i] + ":D";
        i++;
        return {value, done: false}
      }
    }
  };
};


//for in loop
let john = {name: "john", age: 16, job: "student"}

for(let key in john){
  console.log(john[key]);
}



```

Note about For of loop

- only used in iterable object like string, array
- Symbol.iterator control how for of loop
