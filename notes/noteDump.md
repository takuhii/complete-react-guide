# Section 1.3 - Why React Instead of "Just JavaScript"?
See code example in resources/section 1.3

The React version works the same way but looks very different
React is all about splitting your application into small componenets, therefore it is maintainable and manageble

We kind of define what to expect as an end result, and then some placeholders, flexible elements, then very simple "instructions" to change what is visible on the screen. 

These are defined by the react library. It makes building complex, rich, UI easier by giving us a higher level syntax where we write code in a declarative way.

TL:DR > We define the end goal, custom HMTL elements, and react does the rest


# Section 1.4 - Building Single-Page Applications (SPAs) with React
Things get easier with React, when working with React we often build Single Page Apps (SPAs). Because we can use React to control parts of a HMTL page, say a sidebar, and we add a widget to the page.

It is more common to control the entire page with react, which means we use React for EVERYTHING, even for switching ages. So when we clikc on a link and load a new page, it looks to the user like we switched pages, but rather we use react to change what is visible on the screen. This leads to a smoother UI and better experience.


# Section 1.10 - Setting Up the Course Dev Environment
For writing react code, any IDE is recommended, ATOM, Sublime Text, WebStorm, but we recommend VSCode. It is free and amazing.

Once you're opened VSCode, you can tweak the appearance, and open files/folders from there.

Settings/styling, fine tune it to your requirements...

Theme: Dark+
Extensions: (ESLint, Git History, Git Project Manager)

*Prettier*: code formatting (format document > SHIFT + OPT + F), search format in settings, set default formatter to prettier.

*Material Icon Theme*: you don't really need this, but this changes the look of the file icons.














# Section 2.12 - Understanding 'let' and 'const'
These are two keywords we will see and use a lot. `let` and `const` are different ways of creating variables. You've heard of `var` right?

`var` creates a variable in JS, some vars never change technically they are constants. ES6 introduced `let` and `const`, `var` still works, but you are encouraged to use `let` and `const`

`let` is you want to create a variable
`const` for something with a constant value

Code Example
```
var myName = 'Max';
console.log(myName);
```

This will display "Max"
```
var myName = 'Max';
console.log(myName);

myName = 'Manu';
console.log(myName);
```

This will display "Max" and "Manu" respectively.

Now if you chnage `var` to `let` nothing will change
```
let myName = 'Max';
console.log(myName);

myName = 'Manu';
console.log(myName);
```

We still get "Max" and "Manu". However if you chnage let to const, you will get an error.
```
const myName = 'Max';
console.log(myName);

myName = 'Manu';
console.log(myName);
```

```
TypeError: Assignment to constant variable.
```

This is because we tried to re-assign a contant variable, so we get an error, and an opportunity to rewrite your code.



# Section 2.14 - Exports and Imports (Modules)
Another feature of next gen JS is writing modular code. So JS you split up over multiple files. We already can do this, but we have to import them in the correct order.

The idea behind export/import statments and so called Modules, is that inside of a JS file we can import content from another file, so that the JS files themselves know their dependecies

Here is an example;
We have one file, `person.js` and inside it we have
```
const person = {
  name = 'Max'
}

export default person
```
We have a const called person which stores a JS object, and then we EXPORT this, default marks it as the default export for this file.

We might have another file were we export multiple things, `utility.js`
```
export const clean = () => {...}
export const baseData = 10;
```

Here a constant named clean which holds a function, and baseData which holds a humber. In a third file we might need to import from person and utility JS, `app.js`
```
import person from './person.js'
import prs from './person.js'

import { baseData } from './utility.js'
import { clean } from './utility.js'
```

App.js requires import statements, the default keyword simply means if we just import something from a file, it will always be our default export. So as you can see in the example above, we can call this whatever we want, which is why we have written it twice.

TL:DR Imports default and ONLY export of the file. Nmae in the receiving file is up to you

For `utility.js` is is a little different, we import based on the specific named exports which is why we use the curly braces, so we can focus on those specific exports, it can also be written like this
```
import { baseData, clean } from './utility.js'
```

We can do these import and exports in a number of different ways
## default export - we choose the name
```
import person from './person.js'
import prs from './person.js'
```

## named export - name is defined by export
```
import { smth } from './utility.js' 
```

you can asign an alias, which we can freely choose
```
import { smth as Smth } from './utility.js'
```

We can also "bundle" multiple named exports with *
```
import * as bundled from './utility.js'
```

we then refer to them as properties `bundled.baseData`, `bundled.clean` and so on.

# Section 2.15 - Understanding Classes
Classes are essentially blueprints for object, Clases can have both pr0perties and methods. Methods are simply functions attached to classes, wqhere-as properties are variables attached to classes you could say.

An example of a class

```
class Person {
  name = 'Max'
  call = () => { ... }
}
```
Classes are instantiated like this (with the new keyword)
```
const myPerson = new Person()
myPerson.call()

console.log(myPerson.name)
```
You might recognise the new keyword from constructor functions, and classes are a more convenient way of creting constuctor functions.

So we create JS objects with classes as blueprints. Classes also support inheritence, this means you have another class you inherit from taking all its properties and methods and potentially adding new properties and methods. This might also remind you of prototypes.
```
class Person extends Master
```

Let's create a new class as an example
```
class Person {
  constructor () {
    this.name = 'Max'
  }

  printMyName() {
    console.log(this.name);
  }
}

const person = new Person();
person.printMyName();
```
We would see Max in the console... We can also demonstrate how classes inherit by using the following
```
class Human {
  constructor() {
    this.gender = 'male';
  }

  printGender() {
    console.log(this.gender);
  }
}

class Person extends Human {
  constructor () {
    this.name = 'Max';
  }

  printMyName() {
    console.log(this.name);
  }
}

const person = new Person();
person.printMyName();
person.printGender();
```
Because we entend Human, we inheirt the properties of Human as well as what we have created inside of Person, now this will currently generate an error
```
"ReferenceError: Must call super constructor in derived class before accessing 'this' or returning from derived constructor."
```

This is important, as if you are extending another class, and you are implementing a constructor, then you have to add `super()`, as below.
```
class Human {
  constructor() {
    this.gender = 'male';
  }

  printGender() {
    console.log(this.gender);
  }
}

class Person extends Human {
  constructor () {
    super();
    this.name = 'Max';
  }

  printMyName() {
    console.log(this.name);
  }
}

const person = new Person();
person.printMyName();
person.printGender();
```

Now if we run the code, we will see `"Max` and `"male"` in the output.

Obviously we could now go into our person class and chnage the gender to 'female'
```
class Human {
  constructor() {
    this.gender = 'male';
  }

  printGender() {
    console.log(this.gender);
  }
}

class Person extends Human {
  constructor () {
    super();
    this.name = 'Max';
    this.gender = 'female';
  }

  printMyName() {
    console.log(this.name);
  }
}

const person = new Person();
person.printMyName();
person.printGender();
```

and now we will see `"Max"` and `"female"` in the output when we run the code. Even though we still have `male` in the original class. This is just one way of writing components, and we have to remember that classes are blueprints for JavaScript Objects, and are comparable to constructor functions.

# 2.16 Classes, Properties & Methods
Next-gen JS offers a different syntax of initialising Properties and Methods, and it is this more modern syntax we will be going forwards with.

Properties are like 'variables' attached to classes/objects

Methods are like 'functions' attached to classes/objects

We will also use this syntax
```
constructor() {
  this.myProperty = 'value'
}
```
setting up properties in a `constructor` function. there is a more modern approach (ES7 at time of writing), that allows us to setup properties directly in the class `myProperty = 'value'`, so you skip the constructor function call.

Behind the scenes this will still be transformed to use constructor functions, but we have an easier time writing our code.

For methods, the appraoch is pretty similar...
```
myMethod() { ... }
```
now using the next-gen JS way, we use a similar syntax as we did for Properties, we simply think of the method as a property that stores a function as a value, and we end up with this
```
myMethod = () => { ... }
```

The advantage of this is, because we use an arrow function, we have no problems using the `this` keyword, this is also the reason we will be using the next-gen syntax going forwards.

Let's try and apply these syntaxs to our code from earlier...
```
class Human {
  constructor() {
    this.gender = 'male';
  }

  printGender() {
    console.log(this.gender);
  }
}

class Person extends Human {
  constructor () {
    super();
    this.name = 'Max';
    this.gender = 'female';
  }

  printMyName() {
    console.log(this.name);
  }
}

const person = new Person();
person.printMyName();
person.printGender();
```

so first let's get rid of the `constructor` in the `Human` class, and the `this` keyword as well, so we just have `gender = 'male'`
```
class Human {
  gender = 'male';

  printGender() {
    console.log(this.gender);
  }
}

...

```
and we can convert `printGender()` to an arrow function
```
class Human {
  gender = 'male';

  printGender = () => {
    console.log(this.gender);
  }
}

...

```
We still use the `this` keyword in the `console.log` when we reach out to the property. The same rules apply to our `Person` class, we can remove the `this` keyword, and convert printMyName to a arrow function. you'll notice that we also got rid of `super()`, we don't need it, as we are no longer using `constructor`
```
...

class Person extends Human {
  name = 'Max';
  gender = 'female';

  printMyName = () => {
    console.log(this.name);
  }
}

...
```
Our final code will look something like this
```
class Human {
  gender = 'male';

  printGender = () => {
    console.log(this.gender);
  }
}

class Person extends Human {
  name = 'Max';
  gender = 'female';

  printMyName = () => {
    console.log(this.name);
  }
}

const person = new Person();
person.printMyName();
person.printGender();
```
We will see `"Max"` and `"female"` in the output when we run the code.

# 2.17 Spread and Rest Operators
We've learned about classes and arrow functions, let's now look at new operators, specifically the `spread` and `rest` operators. Technically it is one operator `...` Depending on where we use it will dictate whether it is `spread` or `rest`.

The `spread` is used to split up array elements or object properties
```
const newArray = [...oldArray, 1, 2]

const newObject = { ..oldObject, newProp: 5 }
```
So in the first syntax example, we can see that we want to create a new array using all the elements from an old array, and add a 1 and 2 element as well. `...` in front of `oldArray` will simply pull out all the elements and add them to `newArray`, and as we are using square brackets, we can add new elements as well.

The same applies to the object, we simply add `...` in front of `oldObject` to add them as key/value pairs to `newObject`, as we are between curly braces, we can add a new property as well (`newProp: 5`), it is worth pointing out that if the oldObject already contained `newProp` it would be over-written by this.

Let's try the following out, we have an array and want to make a new one, how can we use the `spread` operator to do this?
```
const numbers = [1, 2, 3];
const newNumbers = [...numbers, 4];

console.log(newNumbers);
```
We see [1, 2, 3, 4]

and we can prove this is working by logging `numbers` as well
```
const numbers = [1, 2, 3];
const newNumbers = [...numbers, 4];

console.log(numbers);
console.log(newNumbers);
```
we now see `[1, 2, 3]` and `[1, 2, 3, 4]` in the console.

If we didn't use the `spread` operator we would get
```
const numbers = [1, 2, 3];
const newNumbers = [numbers, 4];

console.log(newNumbers);
```
We would see [[1, 2, 3], 4] in the console when we ran the code.

Another example would be

```
const person = {
  name: 'Max'
};

const newPerson = {
  ...person,
  age: 28
}

console.log(newPerson);
```

We will see that we are taking `oldPerson`, and distributing it into `newPerson`


Now the `rest` operator is the same, but used in a different manner to the `spread` operator.

The `rest` operator is used to merge a list of function arguments into an array, here is an example
```
function sortArgs(...args) {
  return args.sort()
}
```
So `sortArgs` receives an unlimited amount of arguments (1, 2, 3 and so on), with `...` we only write one argument `args`, but we may receive more than one, and they will be all be merged together into an array, so then we can apply array methods to our arguments list.

An example of the rest operator could be as follows
```
const filter = (...args) => {
  return args.filter(el => el === 1);
}
```

We use the built-in filter method on `args`, remmeber the dots are a rest operator and that merges the arguments into an array. `.filter()` will execute a function on every element in the array. So we get our element (`el`) and return `true` or `false` if the element is equal to 1. `===` checks for type and value, remember. `el` has to be a number, and we are doing all of this in an arrow function we pass to the built in `.filter()` method, and has nothing to do with `rest` or `spread` operators. Now we need to log it so we can see it...
```
const filter = (...args) => {
  return args.filter(el => el === 1);
}

console.log(filter(1, 2, 3));
```
When we run the code, we should only see `[1]`, as an array, because we filtered this array, which we created with a rest operator.




# 2.20 Refreshing Array Functions
We already saw filter, sort and map. Now let's say we want to turn an array into one that is dobuled. We can use an array function for this
```
const numbers = [1, 2, 3];
const doubleNumArray = numbers.map()
```

`map()` is a built-in array method, and there are many of them. It basically take the function as an input, and could be an arrow function, is simply executed on each element in the array, in this case `numbers`. So what we get in the end is a number. We then simply return something and in this instance (depends on what function you use), the new value. We willl `return_num * 2;` which in turn will create a new array `doubleNumArray` with `2, 4, 6` in it.
```
const numbers = [1, 2, 3];
const doubleNumArray = numbers.map((num) => {
  return num * 2;
});

console.log(numbers);
console.log(doubleNumArray);

```

# 2.21 Wrap Up
With this we conclude the module and we learned a lot about next-gen JS and some important JS concepts in general. We will meet a lot of things we learned during the course, it's stil JS, just with some more modern features