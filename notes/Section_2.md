# Section 2.13 - Module Introduction
This module is optional, if you know arrow functions, let, const, you can skip this module.

If you know JS, but haven't worked with ES6, then this module is for you.

These next-gen features allow us to write clean and robust react apps.

JS is evolving quickly, and allows developers to do more powerful things.


# Section 2.14 - Starting Project


# Section 2.15 - Adding JavaScript To A Page & How React Projects Differ


# Section 2.16 - React Projects Use a Build Process


# Section 2.17 - "import" & "export"


# Section 2.18 - Revisitng Variables & Values


# Section 2.19 - Revisitng Operators


# Section 2.20 - Revisitng Functions & Parameters


# Coding Exercise 1: Working with Functions


# Section 2.21 - Arrow Functions
An arrow function is a different syntax for creating JS functions, a normal function looks like this;
```
function myFunc() {
    ...
}
```

you might also be aware of the syntax;
```
var myFunc = function() {
    ...
}
```

An arrow function looks like this;
```
const myFunc = () => {
    ...
}
```

Here we are storing it in a const, and on the right side of the equals, that is the arrow function syntax, a list of arguments can be added between the brackets, then the arrow, and then the function body.

Arrow function syntax is a bit shorter, as it lacks the function keyword, and also helps resolve some issues with the `this` keyword.

If you're worked with the `this` keyword in JS before you will know that it doesn't always refer to what you are expecting it to when you write your code. Witht he arrow function, it will always keep it's context at runtime.

Code example
```
function printMyName(name) {
  console.log(name);
}

printMyName();
```

Returns `undefined`, now we give it an arguement
```
function printMyName(name) {
  console.log(name);
}

printMyName('Max');
```

Now it returns `Max`. Now the arrow function equivalent is as follows
```
const printMyName = (name) => {
  console.log(name);
}

printMyName('Max');
```

We also get `Max` as an output. Now the `this` keyword will be used throughout the course, it becomes important once you add functions to objects. Let's explore some alternative to the code example.

So if we only have one argument, we can omit the brackets as below, but it is only valid for ONE argument;
```
const printMyName = name => {
  console.log(name);
}

printMyName('Max');
```

If you have a function that received no arguments, then leaving the space blank is not valid
```
const printMyName =  => {
  console.log(name);
}

printMyName('Max');
```

you have to pass empty paranthesis, like this
```
const printMyName = () => {
  console.log('Max');
}

printMyName();
```

and we will see `Max` in the output again. If we have more than one argument, we do need to wrap it in parenthesis like this.
```
const printMyName = (name, age) => {
  console.log(name, age);
}

printMyName('Max', 28);
```

This will now return `Max` and `28`.


# Section 2.22 - More on Arrow Function Syntax


# Section 2.23 - Revisiting Objects & Classes


# Section 2.24 - Arrays & Array Methods Like map()


# Coding Exercise 2: Array Methods


# Section 2.25 - Destructuring
There is one more next-gen feature we need to cover, and that is destructuring. Destructuring allows you to easily extract array elements or object properties and store them in variables. This may sound similar to the rest/spread operators, but it isn't. as we learned earlier, spread/rest takes all the objects and distributes them in a new array or object. Destructuring allows you to pull out single elements and store them in variables, or Arrays and Objects.

## Arrays
This can be achieved like this
```
[a, b] = ['Hello', 'Max']
console.log(a) // Hello
console.log(b) // Max
```
We can use the strange looking syntax on the left of the equals `[a, b]`, it looks like we are creating an array, but we are not, we are actually assigning the variables `a` and `b` to `Hello` and `Max` respectively.

## Objects
For Object destructuring it is similar syntax but using curly braces
```
{name} = {name: 'Max', age: 28}
console.log(name) // Max
console.log(age) // undefined
```

So in array destructuring, the order defined what property we take, in Object destructring it is the porperty name, so `{name}` would target the name value on the right hand side, and why age would be undefined, as we are not targetting it.

Let's have a little practice.
```
const numbers = [1, 2, 3];
[num1, num2] = numbers;

console.log(num1, num2);
```

We create our array syntax on the left of the equalt and assign it to our numbers array, if we run the code, we will see it logging
```
1

2
```
because we are targetting 1 and 2, if we wanted to target 1 and 3, then we need to do the following
```
const numbers = [1, 2, 3];
[num1, , num3] = numbers;

console.log(num1, num3);
```
and we will get
```
1

3
```


# Section 2.26 - Destructuring in Function Paramter Lists


# Section 2.27 - The Spread Operator


# Section 2.28 - Revisiting Control Structures


# Section 2.29 - Manipulating the DOM - NOT with React!


# Section 2.30 - MUsing Functions as Values


# Section 2.31 - Defining Functions Inside of Functions


# Section 2.32 - Reference vs Primitive Values
If we create a number like this `const number = 1`, this is a primative type, if we create another number `num2` and use `number`
```
const number = 1;
const num2 = number;
```
`num2` will create a copy of `number`, and if we log it, we will see it is `1`
```
const number = 1;
const num2 = number;

console.log(num2);
```

Number, strings and booleans are all primative types, whenever you store a variable in another variable, it will copy the value.

Objects and Arrays are reference types though, we can demonstrate
```
const person = {
  name: 'Max'
}
```
We create a person object, with just a name inside of it. We now create a second person, and log it
```
const secondPerson = person;

console.log(secondPerson);
```
this will output
```
[object Object] {
  name: "Max"
}
```
but it is not a copy of `person`, instead `person` the object is stored in memory, and the const `person` we store a pointer to the place in mmeory, if we then assign `person` to `secondPerson` that pointer is copied, we can demonstrate this this way
```
const person = {
  name: 'Max'
};

const secondPerson = person;

person.name = 'Manu';

console.log(secondPerson);
```
You would expect to see `Max` in the output, but instead we see `Manu`, even though we are primnting the `secondPerson`. So for `secondPerson` the name also changes, the reason is, is it just copied the pointer, which points to the exact same object in memory as `person` does, so if we chnage name for `person`, we automatically change it for `secondPerson`. It is important to remember this, and it is the same for arrays, if you copy an array, and chnage an array element, it will also chnage in the "copied" array. This is important in React, as it can create unexpected behaviour, because you may manipulate one object in the app, then accidentally manipulate the same object elsewhere in the app. we will learn to copy this in an immutable way, which means we copy it, by REALLY copying it, for that we can use a `spread` operator
```
const person = {
  name: 'Max'
};

const secondPerson = {
  ...person
};

person.name = 'Manu';

console.log(secondPerson); // Max
```
this will pull out the properties and the value of the properties and will add it to the newly created object `secondPerson`, now if we run the code, we will see `Max` in the console, and not `Manu`. Now we have created a real copy. If we `console.log(person)` at the same point, we will see `Manu`, because we have changed it after we copied it.
```
const person = {
  name: 'Max'
};

const secondPerson = {
  ...person
};

person.name = 'Manu';

console.log(person); // Manu
console.log(secondPerson); // Max
```

It's important to realise that objects and arrays are reference types and if you reassign them, you are copying the pointer and not the value. If you want to do this in a real copy way, you have to create a new object and copy the properties and not the entire object.


# Section 2.33 - Next-gen JS; A Summary
In this module, I provided a brief introduction into some core next-gen JavaScript features, of course focusing on the ones you'll see the most in this course. Here's a quick summary!

## let & const
Read more about `let`: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let

Read more about `const`: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/const

`let` and `const` basically replace `var`. You use `let` instead of `var` and `const` instead of `var` if you plan on never re-assigning this "variable" (effectively turning it into a constant therefore).

## ES6 Arrow Functions
Read more: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions

Arrow functions are a different way of creating functions in JavaScript. Besides a shorter syntax, they offer advantages when it comes to keeping the scope of the `this` keyword (see here).

Arrow function syntax may look strange but it's actually simple.
```
function callMe(name) { 
    console.log(name);
}
```
which you could also write as:
```
const callMe = function(name) { 
    console.log(name);
}
```
becomes: 
```
const callMe = (name) => { 
    console.log(name);
}
```
Important: 

When having no arguments, you have to use empty parentheses in the function declaration:
```
const callMe = () => { 
    console.log('Max!');
}
```
When having exactly one argument, you may omit the parentheses:
```
const callMe = name => { 
    console.log(name);
}
```
When just returning a value, you can use the following shortcut:
```
const returnMe = name => name
```
That's equal to:
```
const returnMe = name => { 
    return name;
}
```
## Exports & Imports
In React projects (and actually in all modern JavaScript projects), you split your code across multiple JavaScript files - so-called modules. You do this, to keep each file/ module focused and manageable.

To still access functionality in another file, you need `export` (to make it available) and `import` (to get access) statements.

You got two different types of exports: default (unnamed) and named exports:

default => `export default ...;`

named => `export const someData = ...;`

You can import default exports like this:

`import someNameOfYourChoice from './path/to/file.js';`

Surprisingly, `someNameOfYourChoice` is totally up to you.

Named exports have to be imported by their name:

`import { someData } from './path/to/file.js';`

A file can only contain one default and an unlimited amount of named exports. You can also mix the one default with any amount of named exports in one and the same file.

When importing named exports, you can also import all named exports at once with the following syntax:

`import * as upToYou from './path/to/file.js';`

`upToYou`  is - well - up to you and simply bundles all exported variables/functions in one JavaScript object. For example, if you `export const someData = ...` (`/path/to/file.js`) you can access it on `upToYou` like this: `upToYou.someData`.

Classes
Classes are a feature which basically replace constructor functions and prototypes. You can define blueprints for JavaScript objects with them. 

Like this:
```
class Person {
    constructor () {
        this.name = 'Max';
    }
}

const person = new Person();
console.log(person.name); // prints 'Max'
```
In the above example, not only the class but also a property of that class (=> name ) is defined. The syntax you see there, is the "old" syntax for defining properties. In modern JavaScript projects (as the one used in this course), you can use the following, more convenient way of defining class properties:
```
class Person {
    name = 'Max';
}
 
const person = new Person();
console.log(person.name); // prints 'Max'
```
You can also define methods. Either like this:
```
class Person {
    name = 'Max';
    printMyName () {
        console.log(this.name); // this is required to refer to the class!
    }
}
 
const person = new Person();
person.printMyName();
```
Or like this:
```
class Person {
    name = 'Max';
    printMyName = () => {
        console.log(this.name);
    }
}
 
const person = new Person();
person.printMyName();
```
The second approach has the same advantage as all arrow functions have: The `this` keyword doesn't change its reference.

You can also use inheritance when using classes:
```
class Human {
    species = 'human';
}
 
class Person extends Human {
    name = 'Max';
    printMyName = () => {
        console.log(this.name);
    }
}
 
const person = new Person();
person.printMyName();
console.log(person.species); // prints 'human'
```
## Spread & Rest Operator
The spread and rest operators actually use the same syntax: ... 

Yes, that is the operator - just three dots. It's usage determines whether you're using it as the spread or rest operator.

Using the Spread Operator:

The spread operator allows you to pull elements out of an array (=> split the array into a list of its elements) or pull the properties out of an object. Here are two examples:
```
const oldArray = [1, 2, 3];
const newArray = [...oldArray, 4, 5]; // This now is [1, 2, 3, 4, 5];
```
Here's the spread operator used on an object:
```
const oldObject = {
    name: 'Max'
};
const newObject = {
    ...oldObject,
    age: 28
};
```
`newObject` would then be
```
{
    name: 'Max',
    age: 28
}
```
The spread operator is extremely useful for cloning arrays and objects. Since both are [reference types (and not primitives)](https://youtu.be/9ooYYRLdg_g), copying them safely (i.e. preventing future mutation of the copied original) can be tricky. With the spread operator you have an easy way of creating a (shallow!) clone of the object or array. 

## Destructuring
Destructuring allows you to easily access the values of arrays or objects and assign them to variables.

Here's an example for an array:
```
const array = [1, 2, 3];
const [a, b] = array;
console.log(a); // prints 1
console.log(b); // prints 2
console.log(array); // prints [1, 2, 3]
```
And here for an object:
```
const myObj = {
    name: 'Max',
    age: 28
}
const {name} = myObj;
console.log(name); // prints 'Max'
console.log(age); // prints undefined
console.log(myObj); // prints {name: 'Max', age: 28}
```
Destructuring is very useful when working with function arguments. Consider this example:
```
const printName = (personObj) => {
    console.log(personObj.name);
}
printName({name: 'Max', age: 28}); // prints 'Max'
```
Here, we only want to print the name in the function but we pass a complete person object to the function. Of course this is no issue but it forces us to call personObj.name inside of our function. We can condense this code with destructuring:
```
const printName = ({name}) => {
    console.log(name);
}
printName({name: 'Max', age: 28}); // prints 'Max')
```
We get the same result as above but we save some code. By destructuring, we simply pull out the name  property and store it in a variable/ argument named name  which we then can use in the function body.

## Resources for this lecture
next-gen-js-summary.pdf


# Section 2.34 - JS Array Functions
Not really next-gen JavaScript, but also important: JavaScript array functions like `map()`, `filter()`, `reduce()` etc.

You'll see me use them quite a bit since a lot of React concepts rely on working with arrays (in immutable ways).

The following page gives a good overview over the various methods you can use on the array prototype - feel free to click through them and refresh your knowledge as required: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array

Particularly important in this course are:
`map()` => https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map
`find()` => https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/find
`findIndex()` => https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/findIndex
`filter()` => https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter
`reduce()` => https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce?v=b
`concat()` => https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/concat?v=b
`slice()` => https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/slice
`splice()` => https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/splice


# Section 2.35 - JS Array Functions
