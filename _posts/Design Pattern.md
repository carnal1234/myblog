Design Pattern


There are mainly three ways to create objects

- Factory Pattern
- Constructor Pattern
- Prototype Pattern

```js
//Factory Pattern

let peopleFactory = (name, age) => {
  let temp = {};
  
  temp.name = name;
  temp.age = age;
  
  temp.print = () => {
    console.log(`I am ${temp.name} and ${temp.age} years old`);
  }
  
  return temp;
}

let john = peopleFactory('john', 33);
let mary = peopleFactory('mary', 27);
john.print(); //I am john and 33 years old
mary.print(); //I am mary and 27 years old


```

Constructor pattern

```js
//Constructor Pattern

let peopleConstructor = (name, age) => {
  this.name = name;
  this.age = age;
  
  this.print = () => {
  console.log(`I am ${this.name} and ${this.age} years old`);
  }
}

let john = new peopleConstructor('john', 33);
let mary = new peopleConstructor('mary', 27);
john.print(); //I am john and 33 years old
mary.print(); //I am mary and 27 years old

```

Here is the problem.

Both factory and constructor pattern create same copy of print function, which is bad and violate 'dry' code princple

And the solution is using prototype

Prototype is a shared space of that type

We can put stuff in it and all instances of same type can use stuff.


```js
//Prototype Pattern

let peopleProto = function(){

};

peopleProto.prototype.name = "no name";
peopleProto.prototype.age = 0;

peopleProto.prototype.print = function(){
  console.log(`I am ${this.name} and ${this.age} years old`);
}

let john = new peopleProto();
let mary = new peopleProto();
john.name = "john";
john.age = 33;
mary.name = 'mary' //forget to set age
john.print(); //I am john and 33 years old
mary.print(); //I am no name and 0 years old

john.hasOwnProperty('name') //true
mary.hasOwnProperty('name') //false

```

In the case above, mary itself does not have property 'name'. it uses the property in prototype.

So prototype can be used for setting default value and only for common property.


How can we improve it?? we dont want to set name and age by ourselves each time.

```js
//Dynamic prototype Pattern
let peopleDynamicProto = function(name, age){
  this.name = name;
  this.age = age;
  
  if(typeof this.print !== 'function'){
    peopleDynamicProto.prototype.print = function()     {
     console.log(`I am ${this.name} and ${this.age} years old`);
    }
  }
};


let john = new peopleDynamicProto('john', 33);
let mary = new peopleDynamicProto('mary', 27);

john.print(); //I am john and 33 years old
mary.print(); //I am mary and 27 years old

john.hasOwnProperty('name') //true
mary.hasOwnProperty('name') //true
```

