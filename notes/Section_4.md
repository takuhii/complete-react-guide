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
















