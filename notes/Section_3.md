# Section 3.24 - Module Introduction
We have covered what react is and what it is about. An overview or React and why we might want to use it. In this module we will cover what you need to know to build any kind of react app.

Most importantly we will be building componenet driven user interfaces. How to build user interfaces by embracing called components, which in turn is embraced by React.

## Module content
* React Core Syntax & JSX
  We will learn all the base features

* Working with Components
  How we can build our own components with React

* Working with Data
  Most web applications are not about static text, but about outputting or updating some data.

We will build an example project using all the theory we learn during the course. React has a bunch of core features and we need to learn them in some detail to truly understand them.


# Section 3.25 - What Are Componenets and Why Is React All About Them?
React is a JS Library for building user interfaces. HTML, CSS and JS are about building UI. We use libraries like react because it simplifies building those interfaces. If you have a complex UI, React makes it simpler and easier. You will be able to focus on your business logic, rather than the steps to update the page.

React embraces a concept called Components, React is ALL about components. What is a component, we'll come back to that later...

React is all about components because all UI, in the end, are made up of components. All UI, in the end are made up of components. What could be a component?

If we look at the UI of the example project, you might be able to make out some building blocks that make up the interface, look at the expense items, this si the same item repeated, just with deifferent data, the same goes for the chart.

This is what components are, reusable building blocks in your UI. Components are just a combination of HTML, CSS for styling and possibly JS for logic.

We can split a lot of the UI out, in a granular way, to individual components.

## Why components?
* Reusability
  Avoid repetition

* Seperation of concerns
  Keeps codebase small and manageable.

In any programming language, you tend to work with functions, you splityour code into multiple smnall functions, that call each other.


# Section 3.26 - React Code is written in a declarative way
## How is a Component Built?
In general it is about the HTML, CSS and JS, and therefore components are about HTML, CSS and JS. When we work with React, and build components, we combine HTML, CSS and JS to make components, then combine those together to make the UI. CSS does matter, it is not an important part of the process. React components are about combining HTML and JS.

## React and Components
TL:DR React is all about components.

React allows you to create re-usable and reactive components consisting of HTML and JS (and some CSS).

React uses a Delarative approach, this means you don't tell React a certain HTML element should be created and inserted in a specific place, as you would with Vanilla JS. With React you always define the desired end state, and let React figure out the actual JS DOM instructions. So basically, it is Reacts' job to figure out what elements need to be added, removed or updated.

In the end we build our own custom HTML elements.


# Section 3.27 - Creating a React Project
The simplest way to start a react app is to use create-react-app.
It simply create a collection of preconfigured folders, with basic react code files, and more importantly a bunch of confguration files to help build your app). Simply google `create-react-app`. It also gives you a development environment so you can preview your app locally.

You will need node.js to get this up and running. I used v16.3.1 as I got some errors using v15 as outlined in the project video. The modules and dependencies available at the time of writing required `v12, v14 or >=16`.

Once the process has finished open the folder `react-complete-guide` and run `nom start`

We setup VSCode earlier, open VSCode and the folder we just created... you should see a folder structure on the left and the Start Window on the right.

The exact package names and versions will change over time, this won't impact how react works. 

The package.json holds all dependencies of the project, but also a few development dependencies as well... the SRC folder holds the source code we will be working on.

There is a cleaned up version in the Resources folder `resources/section 3.27` unzip the `01-starting-setup.zip` and replace the `react-complete-guide` contents with the new folders you just unzipped. DON'T DELETE EVERYTHING, just over-write for now.

Now go to terminal and hit `ctrl+c` to stop the server

We'll restart it in a minute, we need to restart the server with an automatic preview, go to VSCode and click on the `Terminal > New Terminal` this will open a terminal inside of VSCode, this will now be our default terminal, VSCode will automatically navigate to our project folder.

Now run `npm i` to download and install the packages and dependencies, we didn't do this earlier as `create-react-app` did it for us. As we have replaced this configuration with the one from the Resources folder, we need to download these again.

At the end of the process, you'll now have a `node_modules` folder which holds all our dependencies. DO NOT EDIT OR WORK IN THIS FOLDER!

Once that's done we can run `npm start` again to restart the server. While the code is running, it will watch our code and update automatically.

We should now see `Let's Get Started!` text on `localhost:3000` and this will be our starting point. Now we can start learning React.


# Section 3.28 - The Starting Project
In case we skipped Section 3.27, You can find the files in the Resources folder `../resources/section 3.27`.

1. Extract it
2. Copy it to the `react-complete-guide` folder
3. Open a terminal in VSCode using `Terminal > New Terminal`
4. run `npm i` to add the new dependencies
5. run `npm start` to start the dev server

Resources
* Section Code Snapshots
* 01-starting-setup.zip


# Section 3.29 - Analyzing a Standard React Project
Let's take a look at the `src` folder... This is where we will spend the majority of our time and where we will write most of our React code.

The first thing we notice is that we have two JS and one CSS file, and what we really want to emphasise is that React code is JUST JAVASCRIPT. But we use React features and a bit of special syntax, but ultimately it is all just JavaScript.

## Index.js
This is the first file executed whenever we load `localhost:3000`. It's not exactly our code but a transformed version of it. We will wirte the codee in an easy to read developer way, with some syntaxical sugar of course, as code like this wouldn't run in a browser
```
import ReactDOM from 'react-dom/client';

import './index.css';
import App from './App';

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<App />);
```

Therefore the `npm start` process watches our code, but transforms it also before it reaches the browser. As an example look at the importing of the CSS file
`import './index.css';`, this wouldn't work in regular JavaScript, that would be invalid syntax as you can't import CSS into JS.

We simply tell the npm process that we want to include this CSS in our overall application, which is why they are picked up.

Another example of syntax which is not regular JavaScript syntax is this, `<App />`, it looks like HTML code inside of a JavaScript file, normally this wouldn't work either, but here it does work as it is transformed before it is delivered to the browser.

What is actually happening with `index.js` though? Well...

* we are importing `ReactDom` from `react-dom`, this means we are importing the `ReactDom` object from the `react-dom` third party library which is one of our dependencies. If you look in the `package.json` you see two react dependencies, `react` and `react-dom`, and yes you can think of them as two separate packages, but that is React. When we import either of these libraries we are using React, as you can see in Index.js.
  
  Importing `ReactDom` makes that feature available inside of `index.js` as this is how modern JS works generally.
  
  Let's say you define a feature, a function, in file-a and you want to use it in file-b, then you have to export the feature you want to use in file-a, then import it into file-b.

  We are importing `ReactDom`, because then we are calling a method on it, the `createRoot` method. this create the main hook of the overall user interface we are about to build. It tells react where the application should be placed in the web page. That leads us to the `index.hml` in the public folder, we will rarely work here.

  The `index.html` file is the single file that the browser will load, the single entrypoint that the UI will be rendered into. If we look at the body, we will see a DIV like this `<div id="root"></div>`, this DIV doesn't hold any content but it is the DIV we want to inject our React content into. So in our index.js, it is the DIV `root` that we are looking for when we use `createRoot`, we then store that root object in a const, so we can then tell it what is rendered in that DIV.

* we are importing `App` from the `app.js`. If we are importing a third-party library our one of our own JS files we can leave the `.js` off. this doesn't apply to CSS. We need to bear in mind that in the end `app` is a component.
  
  `app.js` is fairly trivial at the moment, it holds a function, named `App`, and we export the function at the end of the file. As we mentioned earlier, if we have an object in one file and want to use it in another, then we have to export it.

  What is `app.js` actually doing... not much to be honest, it's a function named App with a capital character, and all we do is return something, in this instance HTML code, which is not normal JS, but it does work, as this is a special feature called JSX invented by the React Team. It works because of our overall project setup.


# Section 3.30 - Introducing JSX
We have this JSX code here
```
function App() {
  return (
    <div>
      <h2>Let's get started!</h2>
    </div>
  );
}

export default App;
```

It is basically HTML code inside of JavaScript. JSX stand for JavaScript XML, as HTML is basically XML. This only works though because of the transformation steps we have running behind the scenes, you can see this transformed code if you want to;
* open the `developer tools` in Chrome
* go to the `sources` tab
* Look in the static/js folder
* there should be a number of JS files, look through them, you should see some fairly cryptic code, turns out this is the trasforming code
* In the `main.chunk.js` file, you see a function named App, it looks very different to our function named app, but it is what it has been transformed to by React so the Browser can read it. This way we get the best of both worlds, code that is easy to write, and code that works in the browser.


# Section 3.31 - How React Works
We have our HTML code here in our App function
```
function App() {
  return (
    <div>
      <h2>Let's Get Started</h2>
    </div>
  );
}

export default App;
```

With React we will build our own custom HTML elements. A component is basically a custom HTML element. We do this with a declarative approach, with React we define our desired target state, then React is responsible for generating and running the DOM instructions that update what appears on the screen.

We can see this in the code above. We want to generate a `<DIV>` with a `<H2>` tag with text inside of it on the screen. In `index.js` we render the App component, and inside this custom element we return the HTML code.

Now let's tweak the code and add a paragraph;
```
function App() {
  return (
    <div>
      <h2>Let's Get Started</h2>
      <p>This is also visible!</p>
    </div>
  );
}

export default App;
```

The Dev server will automatically pick up the chnages and update what we see ont he page so we now see the paragraph. We just define it

With regular JavaScript you would have to select the element on the page, for example with `document.getElementById`
```
function App() {
  docuemtn.getElementById('root');
  return (
    <div>
      <h2>Let's Get Started</h2>
    </div>
  );
}

export default App;
```

But then you would not be done, you would have to create a paragraph, and set the `textContent`, then reach out to the DOM and append the new paragraph.
```
function App() {
  const para = document.createElement('p');
  para.textContent = 'This is also visible';
  document.getElementById('root').append(para);
  return (
    <div>
      <h2>Let's Get Started</h2>
    </div>
  );
}

export default App;
```

This is how you would do it in regular JavaScript, and this is called an Imperative approach. An Imperative Approach is giving clear step by step instructions to the browser and the JavaScript.

With React we define the end state and React will generate these instructions behiond the scenes. 

## Coding Exercise #2
Solution:
```
import React from 'react';

// don't change the Component name "App"
export default function App() {
    return (
        <div>
            <h1>Exercise done!</h1>
        </div>
    );
}
```

# Section 3.32 - Building A First Custom Component
We managed to split our expense tracker into a bunch of simple components
* In the cart we have Individual Charts bars
* The Individual expense items
* Form for adding new expense

Let's start with the Expense Item
So it is considered good practice to put each new component in its own file. One file per component, you will end up with dozens of files, but this is normal.

Let's create a Components folder in the source
`src > components`

We DON'T move App.js in their, as this is a special kind of component due to it's role in the application, it's the root component, which means it is the main component being rendered. All other components will weither be nested in App.js or nested somewhere else.

We build a component tree
```
<App />
|
|
|- <Header />
|
|- <Tasks />
      |
      |- <Task />
      |
      |- <Task />
      |
      |- <Task />
```
This where only the top most component is rendered into a signle HTML page.

Now let's add a new file to our components folder called
`ExpenseItem.js`

It is common in React to start witha capital letter, we then CamelCase if we have additional words in the filename. 

Inside the component, we need component that is rendering `Expense Item Data`, so that the filename tell us which kind of logic and HTML code will live inside of this file.

Let's write the code...
How is a component written in React... Well it is just a function, a special kind of function, but just a JS function... So to create our ExpenseItem Function we would...
```
function ExpenseItem() {
  return <h2>Expense Item!</h2>
}
```

So what we have done is create a finction with the same name as our filename. This is standard practice, and created a return object that will contain our data later on, currently it is a `<H2>` so we can see that it is working...

This is our first, very basic, component. But not our final code... We need to export our function with...
`export default ExpenseItem;`

our final example looks like this now
```
function ExpenseItem() {
  return <h2>Expense Item!</h2>
}

export default ExpenseItem;
```

Now we need to import it in another file, but NOT `index.js`. We need to add it to `App.js`
```
import ExpenseItem from './components/ExpenseItem';

function App() {
  return (
      <div>
        <h2>Let's get started!</h2>
        <ExpenseItem></ExpenseItem>
      </div>
    )
}
```


This `import ExpenseItem from './components/ExpenseItem';` tells JS that we are looking for the ExpenseItem file in the components folder which sites nexts to App.js.

Now it is imported we can use it like a HTML element `<ExpenseItem></ExpenseItem>`. The simple rule is that lowercase elements are built-in HTML elements, and uppercase elements are defined by developers. The name we import relates to the name of the component.

## Coding Exercise 3
Solution
```
import React from 'react';
import ExerciseComponent from './ExerciseComponent';

// don't change the Component name "App"
export default function App() {
    return <ExerciseComponent />;
}

ExerciseComponent
import React from 'react';
// Important: Use export default function MyCmp() { ... }, don't define "export default" on a separate line!

export default function ExerciseComponent() {
  return <p>First exercise - done!</p>
}
```

# Section 3.33 - Writing More Complex JSX Code
We've created our first custom compoent and, while not exciting, we've made it ourselves. We're using it in `App.js`, let's make it more exciting... Let's tweak the HTML code in `ExpenseItem.js` that's being returned... Let's expand it to display the Amount of the expense and the date, so we need to write HTML code that displays and structures these pieces of information
```
function ExpenseItem() {
  return <div>Date</div><div><h2>Title</h2><div>Amount</div></div>
}

export default ExpenseItem;
```

Now this produces an error, and I will tell you why, it is because in React we can only have one root element per return statement. If we format the above code so it is readable for a second, we see that we have TWO root elements and that is not allowed...
```
function ExpenseItem() {
  return <div>Date</div>
  <div>
    <h2>Title</h2>
    <div>Amount</div>
  </div>
}

export default ExpenseItem;
```

Why this isn't allowed we will come back to later :) 

`<DIV>Date` and `<DIV>` wrapped around the H2 and child DIV are two elements. A common work around is to wrap this in another DIV
```
function ExpenseItem() {
  return <div>
    <div>Date</div>
    <div><h2>Title</h2><div>Amount</div></div>
  </div>
}

export default ExpenseItem;
```

We'll use another workaround later, but to improve the readability we can do the following
```
function ExpenseItem() {
  return (
    <div>
      <div>Date</div>
      <div>
        <h2>Title</h2>
        <div>Amount</div>
      </div>
    </div>
  );
}

export default ExpenseItem;
```

If you are using VSCode like I am, then you can use the `Format Document` option (CMD + SHIFT + P and type Format Document) to format the code for you.

So now for our Expense data we can specify
```
function ExpenseItem() {
  return (
    <div>
      <div>March 28th 2021</div>
      <div>
        <h2>Car Insurance</h2>
        <div>$294.67</div>
      </div>
    </div>
  );
}

export default ExpenseItem;
```

We can now see that we can have more complicated HTML structures, as the text displays in our preview. Next let's look at some basic styling...


# Section 3.34 - Adding Basic CSS Styling
Regarding styling, we still use CSSm but there's nothing to React specifically. We just add a new CSS file next to the component file.
```
src
|- components
      |- ExpenseItem.css
      |- ExpenseItem.js
```

And we write our CSS in there. Now back in the ExpenseItem.js file we need to one important thing, we need to make our build aware of our css code so that it is used effectively.

It's not, by default, browsing all the files and using them, we have to explicitly tell React, that certain files need to be considered, and we do this by importing it like we did with `ExpenseItem.js` in `App.js`, like this...
```
import './ExpenseItem.css';

function ExpenseItem() {
  return (
    <div>
      <div>March 28th 2021</div>
      <div>
        <h2>Car Insurance</h2>
        <div>$294.67</div>
      </div>
    </div>
  );
}

export default ExpenseItem;
```

Inside the CSS file there are a bunch of classes we can apply to the HTML code.
```
import './ExpenseItem.css';

function ExpenseItem() {
  return (
    <div className="expense-item">
      <div>March 28th 2021</div>
      <div>
        <h2>Car Insurance</h2>
        <div>$294.67</div>
      </div>
    </div>
  );
}

export default ExpenseItem;
```

You'll notiuce we don;t type class, but instead className, but you have to rememebr that this isnt really HTML, it's special JSX syntax, under thr hood it's still JS, that's why most attributes are the same but not all, we use className because class is a reserved word in JavaScript. Let's finish assigning our classes.
```
import './ExpenseItem.css';

function ExpenseItem() {
  return (
    <div className="expense-item">
      <div>March 28th 2021</div>
      <div className="expense-item__description">
        <h2>Car Insurance</h2>
        <div className="expense-item__price">$294.67</div>
      </div>
    </div>
  );
}

export default ExpenseItem;
```

It should look a little nicer in our preview now, but it's still not quite there.


# Section 3.35 - Outputting Dynamic Data & Working in Expressions in JSX
Now we know how to syle out code, but we definitely aren't finished with that yet. Before we dig deept into the final look, let's look at a fairly obvious problem... We'll probably have more than one expense.

Currently we are hard coded with our data, in our final tracker, we're going to need more than one expense. That is one of the core ideas behind components... From a reusability perspective we want to be able to use a component multiple times and currently we can't do that...

Our hardocded data is unrealistic, some data may be hardcoded, but our date and amount would typically be dynamic, which means it isn't hard-coded, we don't have the capabitlity, but we can fake the data in our preview.

Our component is a mixture of HTML, cSS and JAVASCRIPT, but where is our JaavScript let's add some code...
```
import './ExpenseItem.css';

function ExpenseItem() {
  const expenseDate = new Date(2021, 2, 28);

  return (
    <div className="expense-item">
      <div>March 28th 2021</div>
      <div className="expense-item__description">
        <h2>Car Insurance</h2>
        <div className="expense-item__price">$294.67</div>
      </div>
    </div>
  );
}

export default ExpenseItem;
```

Our const is just regular JavaScript, we're using it to create dummy data, but in the future we could use this with realy world data. Let's take it further...
```
import './ExpenseItem.css';

function ExpenseItem() {
  const expenseDate = new Date(2021, 2, 28);
  const expenseTitle = 'Car Insurance';
  const expenseAmount = 294.67;

  return (
    <div className="expense-item">
      <div>March 28th 2021</div>
      <div className="expense-item__description">
        <h2>Car Insurance</h2>
        <div className="expense-item__price">$294.67</div>
      </div>
    </div>
  );
}

export default ExpenseItem;
```

To include this data in our return statemtn we need to use single curly braces `{ ... }`. As well as include data in these braces, we can also run basic JavaScript expressions, for example `{ 1+1 }` and we would see `2` in our preview. We want to refer to our values in our `consts`, we do that like this...
```
import './ExpenseItem.css';

function ExpenseItem() {
  const expenseDate = new Date(2021, 2, 28);
  const expenseTitle = 'Car Insurance';
  const expenseAmount = 294.67;

  return (
    <div className="expense-item">
      <div>{expenseDate}</div>
      <div className="expense-item__description">
        <h2>{expenseTitle}</h2>
        <div className="expense-item__price">${expenseAmount}</div>
      </div>
    </div>
  );
}

export default ExpenseItem;
```

Now in it's current form, the date object will break your App, and you'll see a blank page in your preview. This is because it isn't ready to be viewed yet, we need to pass it through `.toISOString()` first, like this...
```
import './ExpenseItem.css';

function ExpenseItem() {
  const expenseDate = new Date(2021, 2, 28);
  const expenseTitle = 'Car Insurance';
  const expenseAmount = 294.67;

  return (
    <div className="expense-item">
      <div>{expenseDate.toISOString}</div>
      <div className="expense-item__description">
        <h2>{expenseTitle}</h2>
        <div className="expense-item__price">${expenseAmount}</div>
      </div>
    </div>
  );
}

export default ExpenseItem;
```
This gives us a readable Date Object, which we will need to refine later.


# Section 3.36 - Passing Data via Props
How can we make this component reusable? We wil App.js we can add the ExpenseItem again and we get another Expense Item in the preview, but it's not really dynamic as our data is hard-baked...

Think about regular JS, we use functions to split functionality across multiple smaller code-bases, and re-usable functions we can call multiple times. We make these functions reusable by accepting parameters, that allows us to call the same function with different values, making it produce different results, React has the same concept, we can make components reusable by using parameters and props.
```
<App />
|
|- goalItem = 'Finish!'
|
|- <CourseGoalItem />
|
|- <li>goalItem</li>
```

Let's say in your `<App />` you have `goalItem='Finish!'` variable which holds a string of `Finish!`, then we have a custom component (`CourseGoalItem`) which holds a `listItem` where this `goalItem` should be output. We have a custom component which outputs a `listItem` where the `goalItem` should be output dynamically, the problem is the `goalItem` lives in the `App` component not the `CourseGoalItem` component, and to a certain extent it makes the `CourseGoalItem` independent, if it doesn't store the value internally, but we need to find out what's being output by the variable managed in App. We don't have access to the HTML code output by nother component, we can't just send our storeed data there, but we can use props. We can pass data to the custom component by adding an attribute, and inside that component we an get access to all these attributes. Our component will now look something like this...
```
<App />
|
|- goalItem = 'Finish!'
|
|- <CourseGoalItem text={goalItem} />
|
|- <li>{props.text}</li>
```

We building our own custom HTML elements, and just as HTML elemnts can have attribute, it turns out React can also have attributes, props, which stands for properties. We can set properties for our own custom components.

## How does this concept work?
In `ExpenseItem` we have `Date`, `Title` and `Amount`, we'd like to output this here, but we should store it in App.js, and we could go one better and create a expenses array
```
import ExpenseItem from './components/ExpenseItem';

function App() {
  const expenses = [];

  return (
      <div>
        <h2>Let's get started!</h2>
        <ExpenseItem></ExpenseItem>
        <ExpenseItem></ExpenseItem>
        <ExpenseItem></ExpenseItem>
        <ExpenseItem></ExpenseItem>
      </div>
    )
}

export default App;
```

and every expense here is a simple JavaScript object
```
import ExpenseItem from './components/ExpenseItem';

function App() {
  const expenses = [
    { title: 'Car Insurance', amount: 294.67, date: new Date(2021, 2, 28) }
  ];

  return (
      <div>
        <h2>Let's get started!</h2>
        <ExpenseItem></ExpenseItem>
        <ExpenseItem></ExpenseItem>
        <ExpenseItem></ExpenseItem>
        <ExpenseItem></ExpenseItem>
      </div>
    )
}

export default App;
```

but we are going to need more than one...
```
import ExpenseItem from './components/ExpenseItem';

function App() {
  const expenses = [
      {
        id: 'e1',
        title: 'Toilet Paper',
        amount: 94.12,
        date: new Date(2020, 7, 14),
      },
      { id: 'e2', title: 'New TV', amount: 799.49, date: new Date(2021, 2, 12) },
      {
        id: 'e3',
        title: 'Car Insurance',
        amount: 294.67,
        date: new Date(2021, 2, 28),
      },
      {
        id: 'e4',
        title: 'New Desk (Wooden)',
        amount: 450,
        date: new Date(2021, 5, 12),
      },
    ];
  }

  return (
      <div>
        <h2>Let's get started!</h2>
        <ExpenseItem></ExpenseItem>
        <ExpenseItem></ExpenseItem>
        <ExpenseItem></ExpenseItem>
        <ExpenseItem></ExpenseItem>
      </div>
    )
}

export default App;
```

Now we have 4 objects inside of our expenses array, now we need to pass that data to our component.

In App.js we can add attributes to our custom components, for example we can add title to our component.
```
import ExpenseItem from './components/ExpenseItem';

function App() {
  const expenses = [
      {
        id: 'e1',
        title: 'Toilet Paper',
        amount: 94.12,
        date: new Date(2020, 7, 14),
      },
      { id: 'e2', title: 'New TV', amount: 799.49, date: new Date(2021, 2, 12) },
      {
        id: 'e3',
        title: 'Car Insurance',
        amount: 294.67,
        date: new Date(2021, 2, 28),
      },
      {
        id: 'e4',
        title: 'New Desk (Wooden)',
        amount: 450,
        date: new Date(2021, 5, 12),
      },
    ];
  }

  return (
      <div>
        <h2>Let's get started!</h2>
        <ExpenseItem title="Toilet Paper"></ExpenseItem>
        <ExpenseItem></ExpenseItem>
        <ExpenseItem></ExpenseItem>
        <ExpenseItem></ExpenseItem>
      </div>
    )
}

export default App;
```

but this is no good, as we are still hard-coding data, so we can try something else...
```
import ExpenseItem from './components/ExpenseItem';

function App() {
  const expenses = [
      {
        id: 'e1',
        title: 'Toilet Paper',
        amount: 94.12,
        date: new Date(2020, 7, 14),
      },
      { id: 'e2', title: 'New TV', amount: 799.49, date: new Date(2021, 2, 12) },
      {
        id: 'e3',
        title: 'Car Insurance',
        amount: 294.67,
        date: new Date(2021, 2, 28),
      },
      {
        id: 'e4',
        title: 'New Desk (Wooden)',
        amount: 450,
        date: new Date(2021, 5, 12),
      },
    ];
  }

  return (
      <div>
        <h2>Let's get started!</h2>
        <ExpenseItem title={expenses[0].title}></ExpenseItem>
        <ExpenseItem></ExpenseItem>
        <ExpenseItem></ExpenseItem>
        <ExpenseItem></ExpenseItem>
      </div>
    )
}

export default App;
```

We are using the single curly braces again, but this time we are assigning vlues to attributes, from here I can access my expenses array, in our example the first item in the array, title. We can do the same for `Amount` and `Date`...
```
import ExpenseItem from './components/ExpenseItem';

function App() {
  const expenses = [
      {
        id: 'e1',
        title: 'Toilet Paper',
        amount: 94.12,
        date: new Date(2020, 7, 14),
      },
      { id: 'e2', title: 'New TV', amount: 799.49, date: new Date(2021, 2, 12) },
      {
        id: 'e3',
        title: 'Car Insurance',
        amount: 294.67,
        date: new Date(2021, 2, 28),
      },
      {
        id: 'e4',
        title: 'New Desk (Wooden)',
        amount: 450,
        date: new Date(2021, 5, 12),
      },
    ];
  }

  return (
      <div>
        <h2>Let's get started!</h2>
        <ExpenseItem
          title={expenses[0].title}
          amount={expenses[0].amount}
          date={expenses[0].date}
        ></ExpenseItem>
        <ExpenseItem></ExpenseItem>
        <ExpenseItem></ExpenseItem>
        <ExpenseItem></ExpenseItem>
      </div>
    )
}

export default App;
```

We need to make sure the part after the `.` matches your property names defined at the top of the JS file. We can now do this for the other `expenseItems`...
```
import ExpenseItem from './components/ExpenseItem';

function App() {
  const expenses = [
      {
        id: 'e1',
        title: 'Toilet Paper',
        amount: 94.12,
        date: new Date(2020, 7, 14),
      },
      { id: 'e2', title: 'New TV', amount: 799.49, date: new Date(2021, 2, 12) },
      {
        id: 'e3',
        title: 'Car Insurance',
        amount: 294.67,
        date: new Date(2021, 2, 28),
      },
      {
        id: 'e4',
        title: 'New Desk (Wooden)',
        amount: 450,
        date: new Date(2021, 5, 12),
      },
    ];
  }

  return (
      <div>
        <h2>Let's get started!</h2>
        <ExpenseItem
          title={expenses[0].title}
          amount={expenses[0].amount}
          date={expenses[0].date}
        ></ExpenseItem>
        <ExpenseItem
          title={expenses[1].title}
          amount={expenses[1].amount}
          date={expenses[1].date}
        ></ExpenseItem>
        <ExpenseItem
          title={expenses[2].title}
          amount={expenses[2].amount}
          date={expenses[2].date}
        ></ExpenseItem>
        <ExpenseItem
          title={expenses[3].title}
          amount={expenses[3].amount}
          date={expenses[3].date}
        ></ExpenseItem>
      </div>
    )
}

export default App;
```

If we save this and preview it, we don\'t see any chnage, as we haven't finished enabling our props fully yet.

Inside of our `ExpenseItem.js` we need to do something with these received values, how do we access them? Parameters.

In regular JS we use Parameters for passing data into functions, and it's similar for React, we need to expand our function.
```
import './ExpenseItem.css';

function ExpenseItem(props) {
  const expenseDate = new Date(2021, 2, 28);
  const expenseTitle = 'Car Insurance';
  const expenseAmount = 294.67;

  return (
    <div className="expense-item">
      <div>{expenseDate.toISOString}</div>
      <div className="expense-item__description">
        <h2>{expenseTitle}</h2>
        <div className="expense-item__price">${expenseAmount}</div>
      </div>
    </div>
  );
}

export default ExpenseItem;
```
That one parameter will be an object which holds all our values as props, we can name it whatever we like, we usually call it `props`. This makes it clear that this object holds all our values. The keys in the props will be the attributes on our custom element, in our case `title`, `amount`, `date`, and the values, the corresponding values.

To get access to this value we do the following.
```
import './ExpenseItem.css';

function ExpenseItem(props) {
  const expenseDate = new Date(2021, 2, 28);
  const expenseTitle = 'Car Insurance';
  const expenseAmount = 294.67;

  return (
    <div className="expense-item">
      <div>{expenseDate.toISOString}</div>
      <div className="expense-item__description">
        <h2>{props.title}</h2>
        <div className="expense-item__price">${expenseAmount}</div>
      </div>
    </div>
  );
}

export default ExpenseItem;
```

This then goes to our props, and looks for the key `title`, we will then see the `value` of title in our preview. We have to use the name we picked for our attributes. With this in mind we can also output `props.amount` and `props.date.toISOString`.
```
import './ExpenseItem.css';

function ExpenseItem(props) {
  const expenseDate = new Date(2021, 2, 28);
  const expenseTitle = 'Car Insurance';
  const expenseAmount = 294.67;

  return (
    <div className="expense-item">
      <div>{props.date.toISOString}</div>
      <div className="expense-item__description">
        <h2>{props.title}</h2>
        <div className="expense-item__price">${props.amount}</div>
      </div>
    </div>
  );
}

export default ExpenseItem;
```

We can also get rid of those consts at the top of the return
```
import './ExpenseItem.css';

function ExpenseItem(props) {
  return (
    <div className="expense-item">
      <div>{props.date.toISOString}</div>
      <div className="expense-item__description">
        <h2>{props.title}</h2>
        <div className="expense-item__price">${props.amount}</div>
      </div>
    </div>
  );
}

export default ExpenseItem;
```

Props is super important, and if we look at our preview you'll see why.


## Coding Exercise 4
Solution
```
APP.JS
import React from 'react';

import Product from './Product';
import './styles.css';

// don't change the Component name "App"
export default function App() {
    const products = [
    {
      title: 'Product 1',
      amount: "10",
      description: 'First product',
    },
    {
      title: 'Product 2',
      amount: "20",
      description: 'Second product',
    },
  ];
    return (
        <div>
            <h1>My Demo Shop</h1>
            <Product
                title={products[0].title}
                price={products[0].amount}
                description={products[0].description}
            />
            <Product
                title={products[1].title}
                price={products[1].amount}
                description={products[1].description}
            />
        </div>
    );
}

PRODUCT.JS
import React from 'react';

export default function Product(props) {
    return (
        <article className="product">
            <h2>{props.title}</h2>
            <p className="price">${props.price}</p>
            <p>{props.description}</p>
        </article>
    );
}

STYLE.CSS
body {
    font-family: sans-serif;
    margin: 0;
    padding: 3rem;
    background-color: #2d2c2c;
    color: #959090;
}

.product {
    margin: 1rem 0;
    padding: 1rem;
    background-color: #373535;
    color: #e7e4e4;
    border-radius: 8px;
}

.product h2,
.product p {
    margin: 0.5rem 0;
}

.price {
    font-size: 0.75rem;
    color: #bab6b6;
}
```


# Section 3.37 - Adding "normal" JavaScript Logic to Components
Now we've learned about `props` we are technically done with our first component. The `expenseItem` component is now reusable, and we can use this "props concept" to configure it differently every time we use it.

Lets continue working on our component, specificially the date as it's not too pretty at the moment. We;d like to make it look like a calnder date...

We need to chnage the JSX code that outputs the date. SO to start, inside of or date DIV, we want three new DIVs, and they will be structured like this
```
...
<div>
  <div>Month</div> // Responsible for outputting Month
  <div>Year</div> // Responsible for outputting Year
  <div>Day</div> // Responsible for outputting Day
</div>
...
```

To achieve this we need to extract Month, Year and Day from the incoming date, so from the `expenses[...].date` our date prop... How exactly do we do this?

Well we can use a built in method on all date objects in JavaScript called `toLocaleString`, so we are now calling
```
...
<div>
  <div>{props.date.toLocaleString('en-US', {month: 'long'})}</div>
  <div>Year</div>
  <div>Day</div>
</div>
...
```

This just helps us to start outputting date in human readable format, the above shows us that we wish to format the month, in "english", with a long month name (August not Aug).

It is cleaner however to move that declaration to a const and call it in your code instead.
```
const month = props.date.toLocaleString('en-US', {month: 'long'})

<div>
  <div>{month}</div>
  <div>Year</div>
  <div>Day</div>
</div>
...
```

Doing it like this keeps the code lean, and easier to read. We can also do something similar for Year and Day...
```
const month = props.date.toLocaleString('en-US', {month: 'long'});
const day = props.date.toLocaleString('en-US', {day: '2-digit'});
const year = props.date.getFullYear();

<div>
  <div>{month}</div>
  <div>{year}</div>
  <div>{day}</div>
</div>
...
```

We now see a human readable date in our component. Now we need to add some styling, but let's talk about splitting components first...


# Section 3.38 - Splitting Components into Multiple Components
As we work on the react application and components, you will notice that they become bigger and bigger, as you have more logic and JS code within them. That is why React has this component concept, it allows us to split our application into smaller building blocks, where every building block and component is focused on one core task. Then we build our UI by combining these building blocks together. You keep every component smallo and managebale and keep the codebase small and manageable, but can create complex UIs.

We could argue that our component is starting to grow, we could treat our date as a separate component, so let's spilt it up into two;

ExpenseDate.js
```
function ExpenseDate(props) {
  const month = props.date.toLocaleString('en-US', {month: 'long'});
  const day = props.date.toLocaleString('en-US', {day: '2-digit'});
  const year = props.date.getFullYear();

  return (
    <div>
      <div>{month}</div>
      <div>{year}</div>
      <div>{day}</div>
    </div>
  );
}

export default ExpenseDate;
```

This component will be all about rendering the date of an expense. You can see we've created a new function called `ExpenseDate`. We'll move our logic over for calculating the date. We will want to use this component in our `ExpenseItem` component, but first we need to move some more code. We need to return the code to display this information.

Now we can import our new component into our `ExpenseItem`...
```
import ExpenseDate from './ExpenseDate';
import './ExpenseItem.css';

function ExpenseItem(props) {
  return (
    <div className="expense-item">
      <ExpenseDate />
      <div>{props.date.toISOString}</div>
      <div className="expense-item__description">
        <h2>{props.title}</h2>
        <div className="expense-item__price">${props.amount}</div>
      </div>
    </div>
  );
}

export default ExpenseItem;
```

We can write it as a self-closing element as we have nothing between the opening and closing tags.

Now our code is a little leaner, and our component is a little more reusable than before, but our ExpenseDate component needs a date prop, so be able to extract the date and format it. So we need to add the date prop to our ExpenseDate element.
```
import ExpenseDate from './ExpenseDate';
import './ExpenseItem.css';

function ExpenseItem(props) {
  return (
    <div className='expense-item'>
      <ExpenseDate date={props.date} />
      <div className='expense-item__description'>
        <h2>{props.title}</h2>
        <div className='expense-item__price'>${props.amount}</div>
      </div>
    </div>
  );
}

export default ExpenseItem;
```

Now it is worth noting that the `date=` should match the name of your props in `ExpenseDate.js`. You'll need to pass `props.date`, and this can look a little confusing, we are now funneling data through multiple levels of components. Our component tree from earlier is coming to life. We don't just have the app component, but multiple custom components...
```
<App />
|
|
|- <Header />
|
|- <Tasks />
      |
      |- <Task />
      |
      |- <Task />
      |
      |- <Task />
```

The final `ExpenseDate.js` should look like this...
```
import './ExpenseDate.css';

function ExpenseDate(props) {
  const month = props.date.toLocaleString('en-US', { month: 'long' });
  const day = props.date.toLocaleString('en-US', { day: '2-digit' });
  const year = props.date.getFullYear();

  return (
    <div className="expense-date">
      <div className="expense-date__month">{month}</div>
      <div className="expense-date__year">{year}</div>
      <div className="expense-date__day">{day}</div>
    </div>
  );
}

export default ExpenseDate;
```

Doing this is optional, we could have put everything into `ExpenseItem`, but then it would grow with every chnage and become unmanageable.

# Assignment 1 - Time to Practice: React & Component Basics - Solution
Expenses.js
```
import ExpenseItem from './ExpenseItem';
import './Expenses.css';

function Expenses(props) {
  return (
    <div className="expenses">
      <ExpenseItem
        title={props.items[0].title}
        amount={props.items[0].amount}
        date={props.items[0].date}
      />
      <ExpenseItem
        title={props.items[1].title}
        amount={props.items[1].amount}
        date={props.items[1].date}
      />
      <ExpenseItem
        title={props.items[2].title}
        amount={props.items[2].amount}
        date={props.items[2].date}
      />
      <ExpenseItem
        title={props.items[3].title}
        amount={props.items[3].amount}
        date={props.items[3].date}
      />
    </div>
  );
}

export default Expenses;
```

App.js
```
import Expenses from './components/Expenses';

function App() {
  const expenses = [
    {
      id: 'e1',
      title: 'Toilet Paper',
      amount: 94.12,
      date: new Date(2020, 7, 14),
    },
    { id: 'e2', title: 'New TV', amount: 799.49, date: new Date(2021, 2, 12) },
    {
      id: 'e3',
      title: 'Car Insurance',
      amount: 294.67,
      date: new Date(2021, 2, 28),
    },
    {
      id: 'e4',
      title: 'New Desk (Wooden)',
      amount: 450,
      date: new Date(2021, 5, 12),
    },
  ];

  return (
    <div>
      <h2>Let's get started!</h2>
      <Expenses items={expenses} />
    </div>
  );
}

export default App;
```

Expenses.css
```
.expenses {
  padding: 1rem;
  background-color: rgb(31, 31, 31);
  margin: 2rem auto;
  width: 50rem;
  max-width: 95%;
  border-radius: 12px;
  box-shadow: 0 1px 8px rgba(0, 0, 0, 0.25);
}
```

# Section 3.39 - The Concept of Composition ("Children Props")
So now we have components everywhere, Expenses, ExpenseItem and ExpenseDate. But that is fundamentally React :)

We'll learn more features to make all this more performant, in a nutshell though this is all about Components and the props we pass into them. Componewnts are just custom HTML elements, where we combine HTML, JSX and styling, and extra JS logic.

Creating a UI from these building blocks is called composition. What if we wanted to create a component that is just a shell around any other content... At the moment we have very specific components, they are all configured by props. Sometimes though we might need a component where we don't configure via props, but we can pass content between the opening and closing tags.

If we look at our current project, we can see that we have two kinds of boxes or containers, one around all the expense items (grey), and a container around all the expenses list (black). The idea is to have reusable building blocks and avoid code duplication, we also have some style duplication, also maybe HTML duplication. `expenses` has a DIV around our `ExpenseItem` which also has a DIV round it.

Not all DIVs have the same look, but we can still extract the surrounding container DIV and extreact the styles they have in common into a separate component, and we'll name it `card`, this typically means a container look with rounded corners, drop shadows and such.

Card.js
```
import './Card.css';

function Card() {
    return (
        <div className="card"></div>
    );
}

export default Card;
```

Card.css
```
.card {
  border-radius: 12px;
  box-shadow: 0 1px 8px rgba(0, 0, 0, 0.25);
}
```

This will now given us a wrapper we can start using to wrap our common elements, like this;
```
import ExpenseDate from './ExpenseDate';
import Card from './Card';
import './ExpenseItem.css';

function ExpenseItem(props) {
  return (
    <Card className='expense-item'>
      <ExpenseDate date={props.date} />
      <div className='expense-item__description'>
        <h2>{props.title}</h2>
        <div className='expense-item__price'>${props.amount}</div>
      </div>
    </Card>
  );
}

export default ExpenseItem;
```

Now when we preview this, it doesn't look quite right, all our expense items are lost, and the reason is that, out of the box, we can't use custom components as wrappers, having content between opening and closing tags doesn't work like regular HTML, but React has a solution, we need to expand `Card.js` with a special built-in prop...
```
import './Card.css';

function Card(props) {
    return (
        <div className="card">{props.children}</div>
    );
}

export default Card;
```

`{props.children}` is a reserved name, we can't set this explicitly, andf the value of this will always be the content between the opening and closing tags of our component, and when we preview this, we will now see all our `ExpenseItems`, but they still don't look quite right.

We extracted SOME of the styling all the containers had in common, but we need more, they are missing now though, we are setting a className prop on `Card`, but `Card` is a custome component, and it only supports what we tell them to support and we need to tell it to do so.

We can address this in the following way
```
import './Card.css';

function Card(props) {
  const classes = 'card ' + props.className;
  return (
      <div className={classes}>{props.children}</div>
  );
}

export default Card;
```

Now if we preview our code it looks more like the original, before we moved everything our to the `Card` component. It still needs work, but we're getting there ;)

Now we have this framework in place, we can add this to our `Expenses`
```
import ExpenseItem from './ExpenseItem';
import Card from './Card';
import './Expenses.css';

function Expenses(props) {
  return (
    <Card className="expenses">
      <ExpenseItem
        title={props.items[0].title}
        amount={props.items[0].amount}
        date={props.items[0].date}
      />
      <ExpenseItem
        title={props.items[1].title}
        amount={props.items[1].amount}
        date={props.items[1].date}
      />
      <ExpenseItem
        title={props.items[2].title}
        amount={props.items[2].amount}
        date={props.items[2].date}
      />
      <ExpenseItem
        title={props.items[3].title}
        amount={props.items[3].amount}
        date={props.items[3].date}
      />
    </Card>
  );
}

export default Expenses;
```

And now we're back to our original look and feel, we have managed to extract some code duplication, and our code is a little leaner.


# Section 3.40 - A First Summary
This was about components, understanding the most important concept of react, that you build UI building and combining components.

We looked at the React core syntax and JSX, we looked at building and using/working with components and props, we learned how to share data across components.

With all these components we are building, we are just splitting our code across multiple files and building blocks.

One thing we will note is that none of our array data is dynamic, it's all static and we have no chance of interacting with it.

We'll look at JSX next.


# Section 3.41 - A Closer Look at JSX
Opening DEV tools, we can see the JS code that is responsible for displaying our page. We can also see all our functions, including our APP code. You won't see JSX in a browser, but our syntaxical sugar (custom HTML elements) helps with the behind the scenes transformations.

We could write code that is less JSX, but is harder to read...

In `package.json` we have a bunch of dependencies, the two we will concentrate on are `react` and `react-dom`. We are using react-dom in the index.js file, but we never import React anywhere... This works in the project setup related to Create-React-App projects, and the project associated with this course.

We need to `import React from 'react';` in older React projects component files, because JSX is syntaxical sugar, under the hood it is transformed to methods called on the react object, which is why we needed to import it in the past.

Lets see what the code would look like without JSX, using `createElement`, JSX calls this method. `createElement` uses three arguments, the first is the element tobe created, if it is built in, we just pass a string `'div'`, the second argument configures the element, an object which sets all the attributes of the element. The thirs argument is the content, now this isn't just it, we can actually have an infinite number of arguemnts here, depending what we want to place between out two DIVs. If we use the earlier return statment in `App.js` as an example, and recreate it without JSX

```
//  return (
//    <div>
//      <h2>Let's get started!</h2>
//      <Expenses items={expenses} />
//    </div>
//  );

return React.createElement(
  'div',
  {},
  React.createElement('h2', {}, "Let's Get Started!"),
  React.createElement(Expenses, {items: expenses}),
);
```

Now we could write the entire app like this, but it's harder to read.


# Section 3.42 - Organising Component Files















