# Section 1.1 - Welcome to the Course


# Section 1.2 - What is ReactJS?
React is a JavaScript Library for writing User Interfaces

Consider NetFlix. It is highly interactive, easy to ue and we don't wait for anything to load.

Mobile apps give a great highly reactive user experience

Traditionally website don't feel like this... Traditionally, in web apps, you click a link and wait for a new page to load. you click a button and wait for some action to complete...

It's this request and response cycle we can break up with JavaScript

JavaScript allows us to run logic in the browser, JavaScript can manipulate the DOM, we can change what the user sees.

ReactJS is a client side JS library. All about modern, reactive UIs for the web.


# Section 1.3 - ReactJS vs "Vanilla JavaScript": Why Use React?
Often, using just JavaScript isn't a great option, and using libraries like React is better, becuase React offers a simpler "Mental Model" and offers a better way of building complex applications and user interfaces.

You will find two basic web applications in the `resources/section 1.3` which essentially have the same content. One app is built with Vanilla JS and the other with ReactJS, so wa can compare how they work.

Now in the Vanilla JS version we have two important files, the `index.html` and the `index.js` which is responsible for pretty much everything, from getting the correct buttons, listening for when buttons are clicked and updating the UI when we perform an action.

If we look at the React app, we can see that we have the same behaviour, but the code is very different. We have an `index.html` but it is in the `public` folder, and is actually very empty when we compare it to its Vanilla JS counterpart. The `body` section only contains one div, which is empty, and this is because React is responsible for rendering the entire user interface.

It is the `index.js` file in the `src` folder where our React journey starts, but we will learn about that later.

The `App.js` file in the `src` folder contains our important code, in their we have a function called `App`, and in their we see something strange becuase we have a bunch of HTML code in their, which is not a default JavaScript feature as, by default, if you add HTML to a JS file, you will get an error. However it will work in a React project becuase of how it is setup behind the scenes, and we will learn how to do this later on.

If you look at the HTML code in our `App` function, you will see we have everything there that we also had in the Vanilla JS project, except now, it is in one file, and the js instructions (listeners and click events, etc) are missing in the React version, becuase now we have those elements in our HTML, and within that HTML we have some dynamic elements whihc now define the different states within the HMTL elements.

When working with React


# Section 1.4 - Editing Our First React App



# Section 1.5 - About the Course & Course Outline
What to expect from the course and what is covered.

You might have already looked at the curriculum, this is a huge course and it is advised you give it a brief read, as it is always up to date.

This course is organised into 3 main categories

* 1st category deals with the basics of react, stuff you need to know
We will start with key basics, components and building UIs. Also working with events, data; props and state, and the styling of react apps and components. We will also look at React hooks.

We are learning core react features step-by-step

* 2nd category deals with more advanced concepts, but realistically you will need them in a lot of apps.
We will look at working with side-effects, refs and more react hooks. React Context API and Redux, and handling user inout wirh forms, HTTP Requests and custom hooks. We will also look at implementing Routing, deployment, nextJS and more...

* 3rd category deals with summaries and refreshers on certain concepts.
This section contains a Javascript Refresher, this is 100% optional, as well as a ReactJS summary

Theory and Small Demos and examples will of course be used to help further us along, as well as Bigger more realistic course projects.

Plenty of challenges and exercises as well :)


# Section 1.6 - The Two Paths
There are two ways to take this course...

## Standard approach
You simply start at lecture 1 in section 1 then continue lecture by lecture in order

You can skip the JS refresher if you don't need it

Then use the React summary module to summarise what you learn or to refresh knowledge if you want to remind yourself without going through the entire course

## Summary Approach
Simply skip the entire course and go straight to the react summary module at the end, maybe take the JS Refresher module if you need to.

The summary section is built stand alone, so you don't have to do the whole course, if you already know what you are doing and understand the core features of React

You can still revisit the entire course later on.


# Section 1.7 - Getting the Most Out of this Course
Before we get started with React, lets check out a couple of tips and tricks to help us throuhgout the course

* Watch the videos, choose your pace...
* Code along & practice as you go, if we do code together, pause and try rebuilding what we did.
* It is 100% normal that you will face problems or errors, and you will need to find solutions, use the code attachments to help solve the issues and help you debug. Use what you learn, use google to help solve the problems on your own.
* Use the community to help and learn together. The Discord channel is really active.


# Section 1.8 - Join the Online Learning Community
Join our Online Learning Community
Great to have you on board as a student!

This course also comes with free access to our “Academind Community” on [AcadeMind Discord](https://academind.com/community/)

There, you can find like-minded people, discuss issues, help each other, share progress, successes and ideas and simply have a good time!

I believe that you learn the most if you don't learn alone but find learning partners and other people with similar interests. Our community is a great place for this - it's the perfect complimentary resource for this course.

Joining it is of course free and 100% optional!

We'd love to welcome you on board of the community! :-)


# Section 1.9 - Creating React Projects: Browser-based vs Local Development



# Section 1.10 - Creating React Projects Locally



# Section 1.11 - Using CodeSandbox for React Development (No Local Setup Required)



# Section 1.12 - Module Resources

