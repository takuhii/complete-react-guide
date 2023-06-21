# Section 4.45 - Module Introduction
Now we've learned some important basics of React, it is time to take the next step. We're going to look at user interaction and user events (click input etc) and we are going to look at state in React Apps. With React we follow that declarative approach where we define the deisred target state and React takes care of the rest...

But at the moment in our App, we can only build static applications, where the state never changes. Where we always output exactly the same, we don't want that, we want interactive applications that react to clicks by the user and data being entered, and are reactive so the application changes when things happen.

We are going to look at handling events, user events like clicks, and we'll see how that works in React apps, and hpw we can add event handlers and so on.

We are also going to look at how what we see on the screen chnages, that we reach a different target state, and for that we will look at the state concept in React, how we transition from state A to state B if you will...


# Section 4.46 - Listening to Events and Woprking with Event Handlers
If we look at our demo application, it is fairly static. We have out output, and we reach that output with the help of our components, we only have one state in this application though.

Let's look at how we can react to user events before we then look at how such events can trigger a state change. To get started we can look at how clicks on a button might react... so let's add a button to `expenseItem.js`
```
import ExpenseDate from './ExpenseDate';
import Card from '../UI/Card';
import './ExpenseItem.css';

const ExpenseItem = (props) => {
  return (
    <Card className='expense-item'>
      <ExpenseDate date={props.date} />
      <div className='expense-item__description'>
        <h2>{props.title}</h2>
        <div className='expense-item__price'>${props.amount}</div>
      </div>
      <button>Change Title</button>
    </Card>
  );
}

export default ExpenseItem;
```

If we save this, we'll see it in our app, it's not great, but it's a temporary button and we'll remove it later.

We now have a button, per expense item component, and we simply want to chnage the title of the expense item when we click the button. We usually get title this via props, but we want to chnage it whenever we click the button. Turns out this is quite simple... Turns out on all HTML elements we have full access to native DOM events.

If you search for 'HTML button elemt' you'll find an MDN article, and if you clikc on DOM interface, you'll see what other elements/classes this inherits from. You'll also see that the HTML button element is a more specific form the the HMTL element, which is a more specific element of Element which is a more specific form of the node and so on.

If we click on Element, for example, we will see a bunch of events we can listen to. Click and Blur. We can use props to listen for these events. In React we add a special prop to our HTML element, but it's not a prop that sets a value, it is a prop that starts with `on`, React exposes all these default events as props.
```
import ExpenseDate from './ExpenseDate';
import Card from '../UI/Card';
import './ExpenseItem.css';

const ExpenseItem = (props) => {
  return (
    <Card className='expense-item'>
      <ExpenseDate date={props.date} />
      <div className='expense-item__description'>
        <h2>{props.title}</h2>
        <div className='expense-item__price'>${props.amount}</div>
      </div>
      <button onClick="">Change Title</button>
    </Card>
  );
}

export default ExpenseItem;
```

As an example we'll use `onClick`, now we need to define what will happen, we do this by defining a value... In this case we want code that will be executed, so how do we do that? We create a function, all these `on` props/event handler props want a function as a value, which executes when the event occurs. We can create it on the fly...
```
import ExpenseDate from './ExpenseDate';
import Card from '../UI/Card';
import './ExpenseItem.css';

const ExpenseItem = (props) => {
  return (
    <Card className='expense-item'>
      <ExpenseDate date={props.date} />
      <div className='expense-item__description'>
        <h2>{props.title}</h2>
        <div className='expense-item__price'>${props.amount}</div>
      </div>
      <button onClick={() => {console.log('Clicked!')}}>Change Title</button>
    </Card>
  );
}

export default ExpenseItem;
```

And you will see in the DEV Console that `Clicked!` now appears when you click the button. Typically though, we don't want to work with such anonymous functions, and wed be adding code to the JSX unnecessarily. We need to keep the JSX lean, instead we want to define the function before the return, or place the function into a CONST...
```
import ExpenseDate from './ExpenseDate';
import Card from '../UI/Card';
import './ExpenseItem.css';

const ExpenseItem = (props) => {
  // function clickHandler() => {
  // 	console.log('Clicked!!!!');
  // }

  const clickHandler = () => {
  	console.log('Clicked!!!!');
  };
  return (
    <Card className='expense-item'>
      <ExpenseDate date={props.date} />
      <div className='expense-item__description'>
        <h2>{props.title}</h2>
        <div className='expense-item__price'>${props.amount}</div>
      </div>
      <button onClick={clickHandler}>Change Title</button>
    </Card>
  );
}

export default ExpenseItem;
```

I've added the function approach as a comment so you can see that this is really up to preference... You may have noticed that the function is inside of curly braces, this is because if we placed the function inside of parenthesis, the function would be executed straight away when the code is parsed, and it is parsed when the JSX code is returned. It's not executed when the button is clicked on, but when the JSX is evaluated. So we just point to the function, and then React does the rest when the element is clicked.

Now we save it, and we will see `Clicked!!!!` in the DEV console...

If an element supports an event, we can add it in React.


# Coding Exercise 5: Listening to Events
```
import React from 'react';

import './styles.css';
// don't change the Component name "App"
export default function App() {
    const clickHandler = () => {
        console.log('Stored!');
    };
    
    return <button onClick={clickHandler}>Bookmark</button>;
}
```


# Section 4.47 - How Component Functions are Executed.
Reacting to event is an important first step. We want to change the title when the button is clicked, so we could create a VARIABLE using `let` which we name `title`, and it holds the value we find in `props.title`, then we change our JSX code to use the variable `title`.
```
import ExpenseDate from './ExpenseDate';
import Card from '../UI/Card';
import './ExpenseItem.css';

const ExpenseItem = (props) => {
  // function clickHandler() => {
  //  console.log('Clicked!!!!');
  // }

  let title = props.title;

  const clickHandler = () => {
    console.log('Clicked!!!!');
  };
  return (
    <Card className='expense-item'>
      <ExpenseDate date={props.date} />
      <div className='expense-item__description'>
        <h2>{title}</h2>
        <div className='expense-item__price'>${props.amount}</div>
      </div>
      <button onClick={clickHandler}>Change Title</button>
    </Card>
  );
}

export default ExpenseItem;
```

And when we click on the button, we see the same result as before.

Why do this? Well since it is a variable, we could change it, for example, when the `clickHandler` is executed. So when you click the button, we execute the clickHandler function and we can change the title to `Updated!`, we should then see the title change on our screen, shouldn't we?
```
import ExpenseDate from './ExpenseDate';
import Card from '../UI/Card';
import './ExpenseItem.css';

const ExpenseItem = (props) => {
  // function clickHandler() => {
  //  console.log('Clicked!!!!');
  // }

  let title = props.title;

  const clickHandler = () => {
    title = 'Updated!';
  };
  return (
    <Card className='expense-item'>
      <ExpenseDate date={props.date} />
      <div className='expense-item__description'>
        <h2>{title}</h2>
        <div className='expense-item__price'>${props.amount}</div>
      </div>
      <button onClick={clickHandler}>Change Title</button>
    </Card>
  );
}

export default ExpenseItem;
```

Nothing happened... We can hit the button all day long and nothing changes, why does that happen? We know the `clickHandler` is getting triggered, because if we add a `console.log(title);` we see that appearing in the console.
```
import ExpenseDate from './ExpenseDate';
import Card from '../UI/Card';
import './ExpenseItem.css';

const ExpenseItem = (props) => {
  // function clickHandler() => {
  //  console.log('Clicked!!!!');
  // }

  let title = props.title;

  const clickHandler = () => {
    title = 'Updated!';
    console.log(title);
  };
  return (
    <Card className='expense-item'>
      <ExpenseDate date={props.date} />
      <div className='expense-item__description'>
        <h2>{title}</h2>
        <div className='expense-item__price'>${props.amount}</div>
      </div>
      <button onClick={clickHandler}>Change Title</button>
    </Card>
  );
}

export default ExpenseItem;
```

What are we missing? Simply, React doesn't work like this, we need to look into how React actually parses JSX code, and how it renders it.

Keep in mind that your component is a function. A component is a regular function, the only special thing is that is returns JSX. Since it is a function, someone has to call it, we never called our component functions, we just use them like HTML elements in the JSX. The thing is under the hood, this is almost like a function call. By using our components in JSX we make React aware of our component functions, for example, the `ExpenseItem` function, and whenever React evaluates the JSX code it will call these component functions. These component functions then return more JSX code, which is then evaluated up until there is no more JSX code to evaluate. So Rect keeps on calling any component functions it encounters in JSX and calls any functions that those functions might have returned, untill there are no more left.

Using our project as an example, when React executes `Expenses.js`, when React encounters `ExpenseItem` it executes all the JSX code, executing all the functions within it, such as `Card` and `ExpenseDate`, and executing all the functions within those until there are no more left and render to DOM instructions.

This is all started by the `index.js` file which we point towards the App component `App.js`, that's the first component function that is called, and this happens when the React app is loaded, which happens when the page is visited.

React never repeats that, it goes through all of that when the App is initially rendered, but then it is done. However in modern applications, you might want to update what is visible, and we need a way of telling React that something has changed and a component needs re-evaluating, and this is where we use something in React called `State`


# Section 4.48 - Working with "State".
Stae is not a React specific concept, but it is a key concept in React. In our `ExpenseItem`, we have a scenario where we want to use that built in 'state' concept. We have a title that should chnage when the clickhandler executes, it's actually data that should result in the component being re-evaluated and redrawn when the title data chnages. By default regualr VARs are not triggering a re-evaluation. React doesn't care about these things and ignores them, that code executes, but the overall function doesn't execute again. Even if it would re-execute it, the title would stay the same because that's what we initialise it to.

To tell React to run it again, we need to import something else, a named import...
```
import React, { useState } from 'react';
```

We have imported the React object, and now we have a named import, useState, provided by the React library, and we can define values as state, where changes should reflect in the component function being called again. This is really different to regular variables.

How do we use this useState though? Well inside of our component function, we just call `useState`, and `usestate` is a React Hook... There are other hooks, and we'll come to those, but this one is quite important, and all React Hooks can be recognised by the fact they are prefixed with `use`. These hooks must only be called inside of React component functions, they can't be called outside of functions, and also should not be called in nested functions. There is an exception to this rule, but we will come to that later.
```
const ExpenseItem = (props) => {
  // function clickHandler() {}
  useState();

  let title = props.title;

  const clickHandler = () => {
    title = 'Updated!';
    console.log(title);
  }
}
```

`usestate` doesn't work just like that, it needs a default state value, `useState` creates a special kind of variable, one that chnages will lead the component function to be called again, so we can assign a special value, in our case...
```
const ExpenseItem = (props) => {
  // function clickHandler() {}
  useState(props.title);

  let title = props.title;

  const clickHandler = () => {
    title = 'Updated!';
    console.log(title);
  }
}
```

Now our special varible is created, but we need to be able to use it laster in our component, so `useState` returns something, giving ua access to this special variable, it also returns a function which we can then call to assign a new value to. We won't be assigning values using the equal sign, instead we will use the new function. `useState` actually returns an array, where the first value is the variable itself, the second elemnt in the array is the updating function. We can use array destucturing to store both elements or constants.
```
const ExpenseItem = (props) => {
  // function clickHandler() {}
  const [title, setTtile] = useState(props.title);

  let title = props.title;

  const clickHandler = () => {
    title = 'Updated!';
    console.log(title);
  }
}
```

The first element is a pointer at the managed value (so `props.title`), and the second element is a function which we can call to set a new title (so `setTitle`). `useState` always returns an array with two elements. The first element is always the current state value, and the second element is the fucnton for updating that. Now we can tidy up our code a bit...
```
const ExpenseItem = (props) => {
  // function clickHandler() {}
  const [title, setTtile] = useState(props.title);

  const clickHandler = () => {

    console.log(title);
  }
}
```

`{title}` is still valid in the JSX because we have declared it in `useState`
```
...
  <div className='expense-item__description'>
    <h2>{title}</h2>
    <div className='expense-item__price'>${props.amount}</div>
  </div>
...

```

and when we click the button, nothing happens because we haven't changed the state. We're not updating anything.

If we want to update the value, we don't use an equals like we usually would
`title = newValue` we use `setTitle();` as this is what we declared as our function to update the title and pass our new value as an arugument `setTitle('Updated!');`.

But why do we do it this way instead of using an equals? The reason is that calling this function does not just assign a new value to a variable, it is a special variable to begin with, it is managed by React in memory to begin with, and when we call this state updating function, this special var will not just receive a new value, but the component function in which we call it will be executed again. by calling this function, we are telling React we are assigning a new value to this state and that then also tells React to re-evaluate the component, so React will go and execute the component function, and the assiociated JSX code.

If we save the code we will see the title chnage to `Updated!` in the `ExpenseItem`. You'll notice the console logs still show the title before we update it, this is becuase it doesn't change the value right away, but schedules it, so in the next line thereafter the new value isn't available yet. That why we see the old value, even though it was updated before logging, and we do see that it is called again and the updated value is displayed on the screen, that is how React `state` works.


# Coding Exercise 6: Working with State
You're working on a part of an online shop where a discounted price should be displayed on the screen once the user clicked a button.

Your task is to add an event listener to listen for clicks on the button that's already included in the App component.

Upon a button click, the price should change from $100 to $75.

Add a state value to the existing App component function and make sure the state value is both updated upon button clicks and output as part of the JSX code.
```
import React from 'react';

import './styles.css';

// don't change the Component name "App"
// important: In this code editor, use React.useState() instead of just useState()
export default function App() {
    return (
        <div>
            <p>$100</p>
            <button>Apply Discount</button>
        </div>
    );
}
```

The Solution
```
import React, { useState } from 'react';

import './styles.css';

// don't change the Component name "App"
// important: In this code editor, use React.useState() instead of just useState()
export default function App() {
    const [price, setPrice] = React.useState('$100');
    // Outside of the Udemy Code Editor
    // const [price, setPrice] = useState('$100');
    const clickHandler = () => {
        setPrice('$75');
    };
    return (
        <div>
            <p>{price}</p>
            <button onClick={clickHandler}>Apply Discount</button>
        </div>
    );
}
```


# Section 4.49 - A Closer Look at the "useState" Hook.
We've learned about state and that state is a key concept in React. `useState` registers some state, so some value as a state, ofr the component in which it is being called. It registers it for a specific component instance. We use it four times in `ExpenseItem` as we have 4 expense items in `Expense.js`. Every item gets it's own seperate state which is deteached from the other states, so everytime we call it, so a new state is created. So when we click 'change title' in our code example, it only affects the Expense Item it is attached to and doesn't do all of them.

One thing which could be confusing is, why are we using `const`, well keep in mind we aren't assigning a value using the equal sign. To update the value we use the state changing function. The value is managed somewhere else by React. So using a `const` is fine.

The special thing here is that React keeps track of the useState in a given component for the first time, when we call it for the first time ever it will take that arguement as an initial value. If a component is then re-executed, React will not reinitialise this state, and will grab the latest state and give us that instead.

It is important to understand how state works under the hood. In a nutshell using state is quite simple, you register state (`usestate`), you always get back two values (value itself and updating function), you call the updating function whenever the state should change, you use the first element whenever you want to use the state value to output in your JSX. React does the rest...

Without state, our interface would never change.


# Section 4.50 - State can be updated in many ways.
Thus far, we update our state upon user events (e.g. upon a click).

That's very common but not required for state updates! You can update states for whatever reason you may have.

Later in the course, we'll see Http requests that complete (where we then want to update the state based on the Http response we got back) but you could also be updating state because a timer (set with setTimeout()) expired for example.


# Section 4.51 - Adding Form inputs.
Now we know what state is, and we understand how to listen to events, we can work on our example project to turn it more and more into an expense tracker. Let's add the capability to add user input so users can add there own expenses.

To start this we need to add a new component, we'll call it `NewExpense` and a new file called `NewExpense.js`
```
|-- src
    |-- components
        |-- Expenses
        |-- NewExpense
        |   |-- NewExpense.js
        |-- UI
...
```

`NewExpense.js`
```
const NewExpense = () => {
    
};

export default NewExpense;
```

Now we need to return a form, so we can add the following code to start doing that
```
const NewExpense = () => {
    return <div>
      <form></form>
    </div>
};

export default NewExpense;
```

The `<div>` allows us to add some styling later on, but while we are on the subject of styling, let's add some...
```
|-- src
    |-- components
        |-- Expenses
        |-- NewExpense
        |   |-- NewExpense.js
        |   |-- NewExpense.css
        |-- UI
...
```

and make sure we import it once we have populated it...
```
import './NewExpense.css';

const NewExpense = () => {
    return <div>
      <form></form>
    </div>
};

export default NewExpense;
```

Now we can add the styling to the form, by adding the `new-expense` css class we have outlined in our CSS file (N.B. these were already written for the example).
```
import './NewExpense.css';

const NewExpense = () => {
    return <div className="new-expense">

    </div>
};

export default NewExpense;
```

Now we can work on the `form`, but we're going to move it into a separate component, that way we keep the logic separate and the files are lean again...
```
import './NewExpense.css';

const NewExpense = () => {
    return <div className="new-expense">
      
    </div>
};

export default NewExpense;
```

So we create a new JS file called `ExpenseForm.js`, and drop our code in their...
```
const ExpenseForm = () => {
  
};

export default ExpenseForm;
```

and we'll also create some styles as well, we'll call it `ExpenseForm.css`.
```
|-- src
    |-- components
        |-- Expenses
        |-- NewExpense
        |   |-- ExpenseForm.js
        |   |-- ExpenseForm.css
        |   |-- NewExpense.js
        |   |-- NewExpense.css
        |-- UI
...
```

and we'll import it the same way as before
```
import './ExpenseForm.css';

const ExpenseForm = () => {
  
};

export default ExpenseForm;
```

In the `Expenseform.js` we'll return a form element
```
const ExpenseForm = () => {
  return <form></form>
};

export default ExpenseForm;
```

When it comes to struturing the form, we want to gather expense data and let users input a `title`, a `date`, using a date picker and, of course the amount.

So that means we will need three input fields, and we'll put them all in a DIV so they can be styled. We will also add a class of `new-expense__controls` for single inputs (its in the CSS provided), and we'll also add a label and input type of `text`.
```
const ExpenseForm = () => {
  return <form>
    <div className='new-expense__controls'>
      <div className='new-expense__control'>
        <label>Title</label>
        <input type='text'/>
      </div>
    </div>
  </form>
};

export default ExpenseForm;
```

We write the `<input>` as a self closing tag as, in React, you don't place anything between the opening and closing tags, so this is ok...

So this is a basic input form, and these are all default HTML elements, but we will soon add listeners and state management to make it more functional.

Now we need to copy the DIV to create Amount, and add a few addtional atrributes...
```
const ExpenseForm = () => {
  return <form>
    <div className='new-expense__controls'>
      <div className='new-expense__control'>
        <label>Title</label>
        <input type='text'/>
      </div>
      <div className='new-expense__control'>
        <label>Amount</label>
        <input type='number' min="0.01" step="0.01" />
      </div>
    </div>
  </form>
};

export default ExpenseForm;
```

The `min` attribute specifies the minimum value for an input field. There is also a max attribute which defines, you guessed it the maximum value for a field. You can use the max and min attributes together to create a range of legal values.

The `step` attribute specifies the legal number intervals for an input field, So for example, if `step="3"`, legal numbers could be -3, 0, 3, 6, etc...

Now we can add something for the date
```
const ExpenseForm = () => {
  return <form>
    <div className='new-expense__controls'>
      <div className='new-expense__control'>
        <label>Title</label>
        <input type='text'/>
      </div>
      <div className='new-expense__control'>
        <label>Amount</label>
        <input type='number' min="0.01" step="0.01" />
      </div>
      <div className='new-expense__control'>
        <label>Date</label>
        <input type='date' min="2019-01-01" step="2024-12-31" />
      </div>
    </div>
  </form>
};

export default ExpenseForm;
```

By setting the input type to `date` it should give us a date picker automatically, the `min` and `max` just gives us a manageable date range to work with, so we aren't rolling through loads of dates... But later on we may want to apply a filter to allow us to provide specific years.

Now let's create a button so our user can submit their expenses claims
```
const ExpenseForm = () => {
  return <form>
    <div className='new-expense__controls'>
      <div className='new-expense__control'>
        <label>Title</label>
        <input type='text'/>
      </div>
      <div className='new-expense__control'>
        <label>Amount</label>
        <input type='number' min="0.01" step="0.01" />
      </div>
      <div className='new-expense__control'>
        <label>Date</label>
        <input type='date' min="2019-01-01" step="2024-12-31" />
      </div>
    </div>
    <div className='new-expense__actions'>
        <button type="submit">Add Expense</button>
    </div>
  </form>
};

export default ExpenseForm;
```

we set the `button` type to `submit` so that when the button is pressed, it is submitted. That was a lot of work, but now we can use our new form in our `NewExpense` component... So we need to import it and implement it...
```
import ExpenseForm from './ExpenseForm'
import './NewExpense.css';

const NewExpense = () => {
    return <div className="new-expense">
      <ExpenseForm />
    </div>
};

export default NewExpense;
```

Now we need to render this from `App.js`. So we again, need to import and implement our code like this...
```
import NewExpense from './components/NewExpense/NewExpense';
import Expenses from './components/Expenses/Expenses';

...

  return (
    <div>
      <NewExpense />
      <Expenses items={expenses} />
    </div>
  );
}

export default App;
```

So you can see we've replaced the awful `H2` with our shiny new component for recording expenses. We save our work and we should see the Expenses form above the list of expenses.

Now we have added our component, it isn't doing anything and that is what we will look at next...


# Section 4.52 - Listening to User Input.
So lets work on gathering user input. For a start we want to react to every change on every keystroke. To do that we need to add listeners...
```
const ExpenseForm = () => {
  return <form>
    <div className='new-expense__controls'>
      <div className='new-expense__control'>
        <label>Title</label>
        <input type='text' onChange />
      </div>
      <div className='new-expense__control'>
        <label>Amount</label>
        <input type='number' min="0.01" step="0.01" />
      </div>
      <div className='new-expense__control'>
        <label>Date</label>
        <input type='date' min="2019-01-01" step="2024-12-31" />
      </div>
    </div>
    <div className='new-expense__actions'>
        <button type="submit">Add Expense</button>
    </div>
  </form>
};

export default ExpenseForm;
```

This adds an `eventListener` for the `change` event to the input element that is rendered in the DOM. Then we need to point to the code that is executed when that event accours... So let's define that
```
const ExpenseForm = () => {
  const titleChangeHandler = () => {
    console.log('Title changed!');
  };

  return <form>
    <div className='new-expense__controls'>
      <div className='new-expense__control'>
        <label>Title</label>
        <input type='text' onChange={titleChangeHandler} />
      </div>
      <div className='new-expense__control'>
        <label>Amount</label>
        <input type='number' min="0.01" step="0.01" />
      </div>
      <div className='new-expense__control'>
        <label>Date</label>
        <input type='date' min="2019-01-01" step="2024-12-31" />
      </div>
    </div>
    <div className='new-expense__actions'>
        <button type="submit">Add Expense</button>
    </div>
  </form>
};

export default ExpenseForm;
```

Now when we type in the title input, we'll see that action recorded in the `console`. This is great, but we want to get the value the user created, and how can we get that, what are our options? The answer is simple, if you know vanilla JS, if we add an eventListener in Vanilla JS like this...
```
document.getElementById('').addEventListener('click', () => {});
```

So here we are we are adding an event listener to an element, in this instance we are listening for the `click` event, and we are passing the function (the `() => {}` bit) as a second argument, which is basically the same function we pass in the `onChange` prop. The function inside the listener, we automatically get an event object which describes which occured, that's default JS behaviour, and we get that default event object in our `titleChangeHandler`, but we don't have to do anything to get it, since we pass the function to React, through onChnage, React will make sure we get the event object when the change event occurs. If we log the event, we can see what it; doing in the console
```
const titleChangeHandler = (event) => {
    console.log(event);
};
```

The most interesting thing in the response is the `target` field. `target` simply point to the DOM element where the event occurred, so in our case `input`, and in turn the `input` element has a long list of properties that we cab read and set, most importantly though, it has a `value` property, the `value` property holds the current value of the input at the time the event occurred.

That's useful, because we can drill into the target and then the value of the event, so we can get the currently entered value.
```
console.log(event.target.value);
```

When we view the console we should see the values we are typing...


# Section 4.53 - Working with Multiple States.
Our next question is, what do we want to do with the value we are capturing? We want to make sure we store it somewhere, so that when we submit the form we can use that value. We want to gather all the values from all inputs and then combine them into an object when the form is submitted.

One way of storing that value and making sure it survives, we can use state again. We can call `usestate` in `ExpenseForm.js` and call it as the start of the `ExpenseForm` function. We also set the state of our first part of the form to an empty string, but we'll destructure it as well... using a similar naming convention from before, `[currentlyEnteredtitle, functionForUpdatingState]`

```
import React, { usestate } from 'react';

const ExpenseForm = () => {
  const [enteredTitle, setEnteredTitle] = useState('');
  ...
```

So now in `titleChangeHandler` we can just call `setEnteredTitle` and pass `event.target.value` as a parameter and this will be stored in our state...
```
import React, { usestate } from 'react';

const ExpenseForm = () => {
  const [enteredTitle, setEnteredTitle] = useState('');

  const titleChangeHandler = (event) => {
    setEnteredTitle(event.target.value);
  ...
```

Now here we aren't really doing this to update the component, but we are doing to to ensure we are storing this in some variable, which is deteached from the life-cycle of the function... There are other ways, but this suits our needs for now.

We can do the same for the other two inputs
```
...
const [enteredTitle, setEnteredTitle] = useState('');
const [enteredAmount, setEnteredAmount] = useState('');
const [enteredDate, setEnteredDate] = useState('');

const titleChangeHandler = (event) => {
  setEnteredTitle(event.target.value);
};

const amountChangeHandler = (event) => {
  setEnteredAmount(event.target.value);
};

const dateChangeHandler = (event) => {
  setEnteredDate(event.target.value);
};

return <form>
  <div className='new-expense__controls'>
    <div className='new-expense__control'>
      <label>Title</label>
      <input type='text' onChange={titleChangeHandler} />
    </div>
    <div className='new-expense__control'>
      <label>Amount</label>
      <input type='number' min="0.01" step="0.01" onChange={amountChangeHandler} />
    </div>
    <div className='new-expense__control'>
      <label>Date</label>
      <input type='date' min="2019-01-01" step="2024-12-31" onChange={dateChangeHandler} />
    </div>
...
```

You'll notice that we can call useState more than once, they will never interfere with each other. We store strings because by default whenever you listen to the change event for an input, if you read the value, it will always be a string...

Now we have our three state slices, and this is ok, we can have these separate states and manage them seperately. This is a key part of React, but there is a one state approach we can look at...


# Section 4.54 - Using One State Instead (And Which Is Better).
So previously, we had multiple handler functions with multiple state slices, and this is totally normal, but there is another way, and this is down to personal preference, you can argue that all three states are related, therefore the same concept repeated three times. We could also go for one state instead of three, how... byt calling useState once and passing in an onject as a value `useState({});`...
```
const ExpenseForm = () => {
  // const [enteredTitle, setEnteredTitle] = useState('');
  // const [enteredAmount, setEnteredAmount] = useState('');
  // const [enteredDate, setEnteredDate] = useState('');
  useState({});
```

This is important, as it is not a string or a number, and in our object we can group together our three states...
```
const ExpenseForm = () => {
  useState({
    enteredTitle: '',
    enteredAmount: '',
    enteredDate: ''
  });
```

So the logic is kind of the same, but now it is in one state object instead of three separate slices, the only difference is we need to update all three properties instead of one, so we can destructure it like this...
```
const [userInput, setUserInput] = useState({
  enteredTitle: '',
  enteredAmount: '',
  enteredDate: ''
});
```

So when the user enters a title, for example, we call `setUserInput` instead...
```
const titleChangeHandler = (event) => {
  setUserInput({
    enteredTitle: event.target.value,
  })
}
```

but we also have to make sure we don't lose our other data as well, as we will dump the other keys when we update this one, React doesn't merge, it replaces. This one state approach means we are responsible for updating the other data, we manually need to copy the other values we are not updating, we can do this with a spread operator 
```
const titleChangeHandler = (event) => {
  setUserInput({
    ...userInput,
    enteredTitle: event.target.value,
  })
}
```

If you haven't seen this before, this just takes an object, pulls out the key value pairs and adds them to the new object and we can overwrite the ones we want... We can then ensure the current values are maintained. Now we can do this for the other values
```
const titleChangeHandler = (event) => {
  setUserInput({
    ...userInput,
    enteredTitle: event.target.value,
  })
}

const amountChangeHandler = (event) => {
  setUserInput({
    ...userInput,
    enteredAmount: event.target.value,
  })
}

const dateChangeHandler = (event) => {
  setUserInput({
    ...userInput,
    enteredDate: event.target.value,
  })
}
```

Now this code still needs a little tweaking, but both approaches we have covered are fine, you will probably see the "Multiple States" approach more in general use than single state approach, but both are ok to use.


# Section 4.55 - Updating State That Depends on the Previous State.
So we have seen how to use one state instead of multiple states, the way we are updating the state isn't entirely correct, it would work, but in niche cases it would fail. So what is the problem... We're depending on the previous state to update the state, in our case we depned on the previous state because we use one state instead of three, and we are reliant on copying in the other values so we don't lose them. So we depend on the previous states snapshot and overwrite only what we are updating.

Now whenever you update state, and you depend on the previous state, you should do it differently...
```
const titleChangeHandler = (event) => {
  // setUserInput({
  //   ...userInput,
  //   enteredTitle: event.target.value,
  // })
  setUserInput((prevState) => {});
}
...
```

We've passed a function to the function, `setUserInput` in this case and passed in a function to it... It is automatically executed by React and will automatically receive the previous state for the state for which we are calling the updating fucntion. Once we have the previous state snapshot, we need to return the new state snapshot...
```
const titleChangeHandler = (event) => {
  // setUserInput({
  //   ...userInput,
  //   enteredTitle: event.target.value,
  // })
  setUserInput((prevState) => {
    return { ...prevState, enteredTitle: event.target.value };
  });
}
...
```

But why is this approach better than the one we looked at earlier? Both work right? Remember React schedules state updates, it doesn't do them straight away, if you schedule a lot, you could be depending on an outdated or incorrect snapshot if you use the previous approach (previous section). If you use the above approach, React will guarantee that the state snapshot will always be the latest, keepoing all the scheduled state updates in mind, so this is the safest way...

For the purpose of the project will will go back to the multiple states approach...


# Coding Exercise 7: Exercise: Using State with Form Inputs
You're working on a text messaging app and your task is to validate the text entered by a user whilst the user is typing.

If the text message entered is valid (for this example: if it's at least 3 characters long), the text "Valid message" should be displayed below the input field. If it's invalid (i.e., shorter than 3 characters), the text "Invalid message" should be displayed.

```
import React, {useState} from 'react';

import './styles.css';

// don't change the Component name "App"
export default function App() {
    const [text, setText] = useState('Invalid message');

    const textChangeHandler = (event) => {
        setText('Valid message');
    };

    return (
        <form>
            <label>Your message</label>
            <input type="text" min="3" onChange={textChangeHandler} />
            <p>{text}</p>
        </form>
    );
}
```


# Coding Exercise 8: Exercise: Using State based on Older State
Your task is to build a basic counter that should increment whenever the "Increment" button is clicked.

Whilst this task allows you to apply your general knowledge about event handling and state (which you already practiced quite a bit at this point in the course), there's also one crucial new aspect: You should update the state following React best practices!

For the sake of the example, make sure to use `React.useState()`...
This is my solution
```
import React, {useState} from 'react';

import './styles.css';

// don't change the Component name "App"
export default function App() {
    const [counter, setCounter] = React.useState(0);

    const counterChangeHandler = (event) => {
        setCounter(counter + 1);
    };
  
    return (
      <div>
        <p id="counter">{counter}</p>
        <button onClick={counterChangeHandler}>Increment</button>
      </div>
    );
}
```

This is the outlined solution from the module creator...
As a first step, register a new state via React.useState():
`const [counter, setCounter] = React.useState(0);`

As a next step, output the counter state value in the App component's JSX code:
```
return (
  <div>
    <p id="counter">{counter}</p>
    <button>Increment</button>
   </div>
);
```

Next, add the onClick prop to the <button>:
`<button onClick={}>Increment</button>`

The onClick prop should receive a function as a value - hence you must add such a function (e.g., called incrementCounterHandler) to your code:

```
export default function App() {
    const [counter, setCounter] = React.useState(0);
    
    function incrementCounterHandler() {
        // Todo: state updating logic
    }
    
    return (
      <div>
        <p id="counter">{counter}</p>
        <button onClick={incrementCounterHandler}>Increment</button>
      </div>
    );
}
```

The last - yet most important - step is to update the counter state in the best possible way. When updating some state based on its previous value, you should use pass a function to the state updating function (i.e., to setCounter(), in this example). This function automatically receives the previous value and should return the new value:
```
function incrementCounterHandler() {
  setCounter(prevCounter => prevCounter + 1);
}
```

Therefore, the final code should look like this:
```
import React from 'react';
 
import './styles.css';
 
// don't change the Component name "App"
export default function App() {
    const [counter, setCounter] = React.useState(0);
    
    function incrementCounterHandler() {
        setCounter(prevCounter => prevCounter + 1);
    }
    
    return (
      <div>
        <p id="counter">{counter}</p>
        <button onClick={incrementCounterHandler}>Increment</button>
      </div>
    );
}
```


# Section 4.56 - Handling Form Submission.
We spent a lot of time on state, but we aren't doing to much with state, and now we want to make sure our form can be submitted when we press the button, and we gather all our state slices into one object, which we will currently log to the console.

We want to listen for our form being submitted, which we could use a click listener for. But this wouldn't be the best approach in our case, there is a default behaviour built into the browser and forms on web pages, if a button with type submit is pressed inside of a form, the overall form will emit an event to which we can listen, and that is the `submit` event. so we want to do the following...
```
...
const dateChangeHandler = (event) => {
  setEnteredDate(event.target.value);
};

const submitHandler = () => {};

return <form onSubmit={submitHandler}>
...
```

So we have created a new Handler (as we did before), but this time assigned it to the `onSubmit` event attached to the `<form>` itself.

Now the thing here is that, as this is a default browser behaviour, that if you do click the submit button, the page reloads. this is because the page sends a request to the server that hosts the web page, in our case the DEV server, and we don't want that. Instead we want to hand the form submission with JavaScript and combine and collect the data and do something with it. Thankfully we can disable/prevent this default behaviour.
```
const dateChangeHandler = (event) => {
  setEnteredDate(event.target.value);
};

const submitHandler = (event) => {};

return <form onSubmit={submitHandler}>
...

```

We get the event object automatically, and we can call the `preventdefault();` method
```
const dateChangeHandler = (event) => {
  setEnteredDate(event.target.value);
};

const submitHandler = (event) => {
  event.preventDefault();
};

return <form onSubmit={submitHandler}>
...

```

This is built into JavaScript and not React specific, we can prevent the default of the request being sent, which stops it reloading the page also, we can continue to handle the data ourselves.
```
const dateChangeHandler = (event) => {
  setEnteredDate(event.target.value);
};

const submitHandler = (event) => {
  event.preventDefault();

  const expenseData = {
    title: enterdTitle,
    amount: enteredAmount,
    date: new Date(enteredDate)
  };
};

return <form onSubmit={submitHandler}>
...

```

Now we have create an `expenseData` object and can combine all our entered data. If we had used our one state instead of three we would already have a combined object.

We add out `date` data to New Date to parse it into a date object. The property names are down to DEV choice, whereas the data we are passing relates to the state variables we created earlier. If we used a combined approach we might want to remap the property names.

And now we'll just `console.log` what we need...
```
const dateChangeHandler = (event) => {
  setEnteredDate(event.target.value);
};

const submitHandler = (event) => {
  event.preventDefault();

  const expenseData = {
    title: enterdTitle,
    amount: enteredAmount,
    date: new Date(enteredDate)
  };

  console.log(expenseDate);
};

return <form onSubmit={submitHandler}>
...

```

And when we test it we should see the date we entered in each field in the console. In my case I entered `Test`, `12.99` and `12/05/2023` and got the following in the console
```
{title: 'Test', amount: '12.99', date: Fri May 12 2023 01:00:00 GMT+0100 (British Summer Time)}
```

Now we just need to clear the input when the form is submitted


# Section 4.57 - Adding Two Way Binding.
How can we clear those inoputs? That's part of the reason we are using `state` to store our values. We could have also used global variables if we just wanted to persist the values, but by using `state` we have an advantage. We can now implement something called two way binding, which basically means, for inputs, we don't just listen for changes, but we can also pass a new value back to the input so we can reset of change it programatically. How do we do that, well it is quite simple really, we add the `value` attribute to our input
```
<input type='text' value="" onChange={titleChangeHandler} />
```

This sets the internal `value` property, which every input element has, and we can set it to a new value, and in our case we will bind it to `enteredTitle`
```
<input type='text' value="{enteredTitle}" onChange={titleChangeHandler} />
```

This is now two way binding as we aren't just listening to changes in the input to update our state, but also feed the state back into the input, so that when we chnage the state we also change the input, while this sounds like an infinite loop, it actually isn't... 

The advantages of when the form is submitted, for example, we can call `setEnteredTitle` and set it to an empty string, which was out initial state.
```
...
  const submitHandler = (event) => {
    event.preventDefault();

    const expenseDate = {
      title: enteredTitle,
      amount: enteredAmount,
      date: new Date(enteredDate)
    };

    console.log(expenseDate);
    setEnteredTitle('');
  };
...
```

By doing this, we over-ride what the user entered after the form was submitted, and therefore clear the input and we can do this for all the inputs, and remember to add the `value` attribute
```
...
  const submitHandler = (event) => {
    event.preventDefault();

    const expenseDate = {
      title: enteredTitle,
      amount: enteredAmount,
      date: new Date(enteredDate)
    };

    console.log(expenseDate);
    setEnteredTitle('');
    setEnteredAmount('');
    setEnteredDate('');
  };
...
<input type='text' value={enteredTitle} onChange={titleChangeHandler} />
...
<input type='number' value={enteredAmount} min="0.01" step="0.01" onChange={amountChangeHandler} />
...
<input type='date' value={enteredDate} min="2019-01-01" step="2024-12-31" onChange={dateChangeHandler} />
...
```

If we save all this and reload, we should see our values reset when we click `add expense`, and our data is still collected in our object,currently `console.log`.

This is of course another key concept in React, as two way binding is very useful when working with Forms, because it allows you to gather inpur and chnage it as well for example, upon form submission ;)


# Section 4.58 - Child-to-Parent Component Communication (Bottom Up).
With the changes we made so far, we are able to gather our expense data into our object and clear the form data when we are done with it.

Having our clearing data is nice, but we don't technically need it in our component, really it should be in the `App.js` because this is where our expenses array is, and our goal is to add our new expense to our list of existing expenses, and enrich it by adding an ID. We need to pass the data to the App component, and currently we have only passed data DOWN, but what about passing it back UP using `Props`? how do we pass data we generate in our components, back up to the `App.js`? We've already used it, so let's re-cap...

In `ExpenseForm.js` we are listening to user input, to chnages to the title for example, whenever the user types there, our function `titleChangeHandler` executes and then we get our default event object, this is something the browser gives us. We can think of the input element as a component, it's not one of ours, but a pre-built one provided by React and translated to the input DOM element. It has component characteristics, and we can set props on it including our `onChnage` prop. `onChange` isn't that special, it's just a prop named `onChange` that want's a function as a value, then our inout element adds an `eventListener` and React sees that we have set a vlaue on the `onChange` prop and adds the listener to the rendered input element.

This is a pattern we can replicate for our own components as well. We can call our own event props, and we can expect functions as values, and that would allow us to pass a function from a parent to a child and then call that function inside the child component, and when we call the function we can pass data to it as a parameter, and that is how we can communicate up... Let's take a quick look

Let's say we want to pass `ExpenseData` which we gathered in `ExpenseForm` and pass it to the new expense component as a first step. Ultimately, if we want to reach the `App.js` we need to reach the `NewExpense.js` component first, and this is because it is the `NewExpense.js` component that uses the `ExpenseForm`. In a second step later on, it is the App component that uses the `NewExpense` component.

We can't skip components in between, this is something we covered earlier, props can only be passed from Parent to Child, we can't skip intermidiate components. So as a first step, let's make sure we can pass the `Expense` data to `NewExpense`, we can do this by adding a new prop to `<ExpenseForm />`, it is out component, so we can call it what we like, in this instance we will call in onSaveExpenseData

```
const NewExpense = () => {
  return <div className="new-expense">
    <ExpenseForm onSaveExpenseData />
  </div>
};
```

If you rememeber what we said about props earlier, naming this `on...` indicates we are expecting a function, a function that is triggered when something happens inside of our component, in this case (and indicated by our name) when the user saves the entered expense data, so when the form is submitted. We can call this prop whatever we want though, we're just trying to standardise things here ;)

Now we have named our prop, we need to define it, and in this case, we need to define it in `NewExpense.js`...
```
const saveExpenseDataHandler = (enteredExpenseData) => {}

const NewExpense = () => {
  return <div className="new-expense">
    <ExpenseForm onSaveExpenseData />
  </div>
};
```

Using the ocnventions we've learned, we have create a new `const` called `saveExpenseDataHandler` and expected `enteredExpenseData`, we can name this whatever we like, but let's keep it simple for now... We have now made it quite clear that this function expects this parameter `enteredExpenseData`. Now we can add our `expenseData`...
```
const saveExpenseDataHandler = (enteredExpenseData) => {
  const expenseData = {};
};

const NewExpense = () => {
  return <div className="new-expense">
    <ExpenseForm onSaveExpenseData />
  </div>
};
```

and copy in our `enteredExpenseData`...
```
const saveExpenseDataHandler = (enteredExpenseData) => {
  const expenseData = {
    ...enteredExpenseData
  };
};

const NewExpense = () => {
  return <div className="new-expense">
    <ExpenseForm onSaveExpenseData />
  </div>
};
```

We expect this to be the object we generate in the `submitHandler`
```
...
const submitHandler = (event) => {
  event.preventDefault();

  const expenseDate = {
    title: enteredTitle,
    amount: enteredAmount,
    date: new Date(enteredDate)
  };
...
```

By using the spread operator, we have pulled out all the key/value pairs. and added a new key called `ID` and assing `Math.ranoom().toString()` to generate a unique value and convert it to a string...
```
const saveExpenseDataHandler = (enteredExpenseData) => {
  const expenseData = {
    ...enteredExpenseData,
    id: Math.random().toString();
  };
};

const NewExpense = () => {
  return <div className="new-expense">
    <ExpenseForm onSaveExpenseData />
  </div>
};
```

It's not a perfect approach to generate an id, but it will suffice for this project, and then we just log the `expenseData` for now
```
const saveExpenseDataHandler = (enteredExpenseData) => {
  const expenseData = {
    ...enteredExpenseData,
    id: Math.random().toString();

    console.log(expenseData);
  };
};

const NewExpense = () => {
  return <div className="new-expense">
    <ExpenseForm onSaveExpenseData />
  </div>
};
```

Now it's a pointer to this function, `saveExpenseDatahandler` that we want to pass as a value through `onSaveExpensedata`...
```
const saveExpenseDataHandler = (enteredExpenseData) => {
  const expenseData = {
    ...enteredExpenseData,
    id: Math.random().toString()
  };
  console.log(expenseData);
};

const NewExpense = () => {
  return <div className="new-expense">
    <ExpenseForm onSaveExpenseData={saveExpenseDataHandler} />
  </div>
};
```

So now our prop, receives our function as a value, but we don't execute, we just point, this way the function is passed to `ExpenseForm`, that is the first step, the second step is to use that function inside of our component... That is a step we didn't have to do for the inputs as these are built in components, but we still passed a function to `onChange` and React will add a listener and call the function we pass in when the event occurs, now we are doing this on our custom component, we also have to call the passed in function manually, and that is what we will do next.

So inside of `ExpenseForm` we can expect our `onSaveExpenseData` prop because we are setting it when we use the `ExpenseForm` component, and in turn, we can extract the value passed through our `onSaveExpenseData` prop, i.e. our `saveExpenseDataHandler` function.

So inside of `ExpenseForm` we do expect to get some props, because we are setting one now...
```
const ExpenseForm = (props) => {
```

And inside of the `submitHandler` instead of logging our expense data we will access it like this, and execute it here...
```
const submitHandler = (event) => {
    event.preventDefault();

    const expenseDate = {
      title: enteredTitle,
      amount: enteredAmount,
      date: new Date(enteredDate)
    };

    props.onSaveExpenseData();
    setEnteredTitle('');
    setEnteredAmount('');
    setEnteredDate('');
  };
```

This is important, now we are executing it, and the reason we can execute it is because the value we are receiving is a function, it is this function below, that we are executing in a different component.
```
const saveExpenseDataHandler = (enteredExpenseData) => {
  const expenseData = {
    ...enteredExpenseData,
    id: Math.random().toString()
  };
  console.log(expenseData);
};
``` 

And we can execute this funtion because we are passing a pointer to it throuhg our `onSaveExpenseData` prop. This is a really important pattern you will use a lot in React. This is how you communicate between components, and this is how you communicate up and how you can make sure the child component can communicate up to the parent component. We can call our function in the `NewExpense` component and pass data as a parameter, when we call `onSaveExpenseData`, we can pass the data as an arguement, and that is the value which we receive in `NewExpense`, and when we run that in our preview, we should see this in the console...
```
{title: 'Test', amount: '12.99', date: Mon May 15 2023 01:00:00 GMT+0100 (British Summer Time), id: '0.7345974439598604'}
```

And we can see that this is being logged from our `NewExpense` file, line 10 (depends on how you format your file though). Now we can continue as we are and communicate from `NewExpense` to `App`, purely because it is the App component that needs to add  our new expense to the Array. We can do this by adding a new function...
```
...
const addExpenseHandler = expense => {
  console.log('In App.js!');
  console.log(expense);
};

return (
  <div>
...
```

So here we expect to get our expene as a parameter, and then we expect to do something with it, so we'll `console.log` it for now, as we haven't learned how to handle this data properly yet. So now, as before, we need to add a point to `NewExpense`, so we can pass our data around, now we add a prop to `NewExpense`...
```
...
<NewExpense onAddExpense={addExpenseHandler} />
...
```

Inside of `NewExpense` we can call it... We can set `NewExpense` to receive our props, and add `props.onAddExpense();` so we are calling the function passed as a value for the `onAddExpense` prop. We make sure to forward our enriched data (remember the `id` we added) to the prop.
```
const NewExpense = (props) => {
  const saveExpenseDataHandler = (enteredExpenseData) => {
    const expenseData = {
      ...enteredExpenseData,
      id: Math.random().toString()
    };
    props.onAddExpense();
  };

    return <div className="new-expense">
      <ExpenseForm onSaveExpenseData={saveExpenseDataHandler} />
    </div>
};
```

If we save and reload, we should see our `console.log` message and our new expense logged to the console also.
```
In App.js!

{title: 'Book', amount: '12.99', date: Mon May 15 2023 01:00:00 GMT+0100 (British Summer Time), id: '0.05349438493545611'}
```


# Section 4.59 - Lifting The State Up.
We've learned about a very important concept of moving data from a child to a parent component by utilising props to receive a function from the parent which we call in the child component. This is closely related to another key concept we have already used without even knowing, and that is a concept called lifting state up.

Consider this basic component tree
```
<App />
|
|- <Expenses />
|
|- <NewExpense />
```

This is basically our demo application, where we have an App component, which in turn renders an Expenses and New Expenses component. Now in this case the `<NewExpense />` component does generate some data, some state.
```
<App />
|
|- <Expenses />
|
|- <NewExpense />
   Data/State is generated here
```

In our sample application we are fetching some user input, and it is quite common to generate or fetch data in a component, but you might not need that data in that component, and we need that data/state in another component
```
<App />
|
|- <Expenses />
|  Data/State is needed here
|
|- <NewExpense />
   Data/State is generated here
```

This is where we need our generated data in the end, slightly transformed and packed into an onject, but it is our generated data non the less... Naturally we would like to hand that data over, but as we have no direct connection between two sibling components (`Expenses and NewExpense`), this isn't possible. As we have currently seen, we can only communicate from Parent to Child and Child to Parent. That is why we use a parent component that has direct or in-direct access to both involved components. In our case the `App` component.
```
<App />
This component has access to both involved components
|
|- <Expenses />
|  Data/State is needed here
|
|- <NewExpense />
   Data/State is generated here
```

Our `App` component has access to both components because it renders them both in it's JSX code, that's why we want to utilise that... Because we can now store our state in that closest involved component (in our case, `App`), by lifting our state up, by passing out generated state data from `newExpesne` to `App`. And we are already doing this in our demo application by utilising `Props`. By calling the function we receive on the `onAddexpense` prop, that alone doesn't lift the state up, it just calls a function we receive through props, but then we do something important, we pass data through to function we call here, we pass the expense data to the function we received on the `onAddExpense` prop. By doing that we are lifting the data/state up to the `App` component, so we can use it, like in `addExpenseHandler` where we log it to the console. We aren't yet managing that data as state, we're just logging it, but we will manage it as state later on...

We are already passing that down to the `expenses` component, as that is another part of that lifiting the state concept. We are lifting it up, we are passing it to the parent, because we either need it in the `App` component or pass it down to another component.

We will hear this term quite a bit, and whenever we hear that is is about moving data from a child component to a parent or to pass it down to another child component.

This does not work if you have an app that interacts with two child components.

In our example, it is the `ExpenseForm` that generates the data, it is that component that works with state and stores user input, it then passes it up to `newExpense` component, then we lift it further to the `App` component.

























