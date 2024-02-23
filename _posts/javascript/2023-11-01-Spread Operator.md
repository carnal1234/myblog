---
title: What is spread operator in JS
date: 2023-11-01
tags:
  - Javascript
categories: Javascript
---

In ES6, Javascript introduce ```...``` spread operator to allow an iterable such as array or string to be expanded.  The spread operator is commonly used to make deep copies of JS objects. When we have nested arrays or nested data in an object, the spread operator makes a deep copy of top-level data and a shallow copy of the nested data

Spread operator

```js
const arr1 = [1,2,3,4];
const arr2 = [5,6,7,8];
const arr3 = [...arr1, ...arr2, 9, 10];
const arr4 = [-1, 0, ...arr3, 11, 12]
console.log(arr3); //[1,2,3,4,5,6,7,8,9,10]
console.log(arr4); //[-1, 0, 1,2,3,4,5,6,7,8,9,10,11,12
console.log(Math.max(...arr4)); //12
```

Be careful. The spread operator will deep copy the top-level elements of `array1` but shallow copy the nested arrays.

```js
let arr5 = [1, 2, 3, ["Hello", "World"], [4, [5]]];
let arr6 = [...arr5];
arr5[0] = 99;
arr5[3][1] = "Brian";
console.log(arr5) //[99, 2, 3, ["Hello", "Brian"], [4, [5]];
console.log(arr6) //[1, 2, 3, ["Hello", "Brian"], [4, [5]];
```

To avoid this, we can use recursion to deep clone array.

```js
let clone = (items) => items.map(item => Array.isArray(item) ? clone(item) : item);

let arr5 = [1, 2, 3, ["Hello", "World"], [4, [5]]];
let arr6 = clone(arr5)
arr5[0] = 99;
arr5[3][1] = "Brian";
console.log(arr5) //[99, 2, 3, ["Hello", "Brian"], [4, [5]];
console.log(arr6) //[1, 2, 3, ["Hello", "World"], [4, [5]];

```


 We can't use it as object as it is not iterable and cannot be spread. But we could destruct it and combine multiple object into new one.

```js
const obj = { key1: "value1" };
const obj2 = {key2: "value2"};
const array = [...obj, ...obj2]; // TypeError: obj is not iterable
const new_obj = {...obj, ...obj2}//{ key1: 'value1', key2: 'value2'}
```


---
Rest operator, is converse to the spread operator. while the spread operator expands elements of an iterable, the rest operator compresses them into array.

It is commonly used in as function argument
```js
function name(...arguments) {
    statements;
}
```

Note: The Rest parameter should always be at the end in the parameter list, else it causes an error.

On the other hand, rest operator could be used to destruct before assignment

```js
// Define a destructuring array with two regular variables  
// and one rest variable:  
const [productID, produceName, prodductAddress, ...productInfo] = [  
"🍎", "Apple", "Japan", "Shipped directly by plane", "Shelf life is 1 month"  
];  
  
// Invoke the otherInfo variable:  
console.log(productInfo);  
  
// The invocation above will return:  
["Shipped directly by plane", "Shelf life is 1 month"]
```
---
## Push vs Spread operator

Both push and spread operator could add new element into array. But one of the main difference is that `Array.push` adds an element to the end of the existing array while the spread operator creates an entirely new array
- Push **mutate** the original array
- Spread operator create new array

```js
arr = [1, 2, 3]
arr.push(4)
arr2 = [...arr, 5, 6];
console.log(arr) //[1, 2, 3, 4]
console.log(arr2) //[1, 2, 3, 4, 5]
```

## Avoiding mutations

Mutations can have unexpected consequences. If you change something in a collection early in the code, you can create a bug much deeper. Mutations may not always cause major headaches, but they do have that potential, so it’s best to avoid them when possible.

Let take a look at the following example.
```js
// Objects

const pikachu = { name: 'Pikachu 🐹'  };
const stats = { hp: 40, attack: 60, defense: 45 }



'Bad Object Code 💩'

pikachu['hp'] = stats.hp
pikachu['attack'] = stats.attack
pikachu['defense'] = stats.defense

// OR

const lvl0 = Object.assign(pikachu, stats)
const lvl1 = Object.assign(pikachu, { hp: 45 })
console.log(pikachu) //{name: 'Pikachu 🐹', hp: 45, attack: 60, defense: 45}
console.log(lvl0)// {name: 'Pikachu 🐹', hp: 45, attack: 60, defense: 45}
console.log(lvl1) //{name: 'Pikachu 🐹', hp: 45, attack: 60, defense: 45}

'Good Object Code ✅'

const lvl0 = { ...pikachu, ...stats }
const lvl1 = { ...pikachu, hp: 45 }
console.log(pikachu) //{name: 'Pikachu 🐹'}
console.log(lvl0) //{name: 'Pikachu 🐹', hp: 40, attack: 60, defense: 45}
console.log(lvl1) //{name: 'Pikachu 🐹', hp: 45}


```

In bad code example, ```Pikachu``` is directly mutated when we use `Object.assign`.  We accidentally mutate `Pikachu` and create 3 deep copy of it.

```js
'Bad Object Code 💩'
pikachu === lvl0 //True
lvl0 === lv1 // True
```

To avoid this, we could use spread operator to destruct object and create a new object directly.
```js 
'Good Object Code ✅'
pikachu === lvl0 //False
lvl0 === lvl1 // False
```

Let look at one more example about array. As we mentioned before, ```push```
would mutate the original array. It is better to avoid mutation and use spread operator instead.

```js
// Arrays

let pokemon = ['Arbok', 'Raichu', 'Sandshrew'];

'Bad Array Code 💩'

pokemon.push('Bulbasaur')
pokemon.push('Metapod')
pokemon.push('Weedle')

'Good Array Code ✅'

// Push 
pokemon = [...pokemon, 'Bulbasaur', 'Metapod', 'Weedle']

// Shift

pokemon = ['Bulbasaur', ...pokemon, 'Metapod', 'Weedle', ]
```

## Conclusion

Normally It is a good practice to avoid mutation when you handle data. But keep reminding that creating new large array frequently may have performance issue. So It’s crucial to strike a balance between code readability and performance. 

In most situations, the performance impact of using the spread operator and rest parameters is negligible, and the readability and maintainability benefits they provide often outweigh any minor overhead. 

That it for today. Thank you.