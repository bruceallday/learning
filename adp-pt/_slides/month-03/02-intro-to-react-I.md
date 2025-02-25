---
layout: slidedeck
title: Introducing React I Slides
---

{% highlight html %}
name: inverse
layout: true
class: center, middle, inverse

---

# Introducing React

.title-logo[![Red logo](/public/img/red-logo-white.svg)]

---

layout: false

# Agenda

1.  What is React, and why use it?
2.  Key concepts in React
3.  Creating a React app
4.  Working with components

---

template: inverse

# What is React?

???

- Start the lesson with a Think-Pair-Share exercise about the pre-work

---

class: center, middle

.large[
React is a JavaScript **library** for building user interfaces.
]

---

# Why Use React?

React makes it easier to reason about, construct, and maintain _stateless_ and _stateful_ UIs. Specifically, it is:

- **Declarative:** We program the _what_ not the _how_
- **Component-Based:** We build encapsulated pieces of UI to build larger more complex UIs
- **Learn Once, Write Everywhere:** React makes no assumption about how it will ultimately rendered, so we can use it for SSR with Node or to build mobile apps with React Native too

---

# Who Uses React?

- Facebook (created it)
- Instagram
- Netflix
- Alibaba
- Atlassian
- [...and many more!](https://github.com/facebook/react/wiki/Sites-Using-React)

---

template: inverse

# Key Concepts: Components, JSX & the Virtual DOM

---

# Components

Because React is a **component-based view abstraction**, we need to start thinking about our UIs in terms of _components_.

A component may be an input, a button, a list item, etc. It can also be anything wrapping a number of components to create a more complex piece of UI.

We have to think carefully about how we will **manage state** in our components.

---

class: center, middle

.inline-images-border[
![React mock-up](/public/img/slide-assets/thinking-in-react-mock.png)
]

.footnote.right[Image source: [Thinking in React](https://facebook.github.io/react/docs/thinking-in-react.html)]

---

class: center, middle

.inline-images-border[
![React components](/public/img/slide-assets/thinking-in-react-components.png)
]

.footnote.right[Image source: [Thinking in React](https://facebook.github.io/react/docs/thinking-in-react.html)]

---

# Exercise 1

We're going to build a to-do app together with React...

See the [lesson page](/lesson/02-intro-to-react/) for more details.

---

class: center, middle

.large[
**Insight:** React components are the programatic abstraction that makes it possible to create these chunks of UI.
]

---

# Elements & Components

React _elements_ are simply **JS objects used to describe how the HTML for the component should look **, i.e. it is an object-based representation of a DOM node. There are no methods on the object, just data.

They can be created with plain JS or **JavaScript XML (JSX)**.

React _components_, on the other hand, are **functions or classes that return React elements**.

We use `ReactDOM.render()` to render a React element into a particular DOM element, and the return value of this method is the React component instance.

---

# React Elements

What a React element looks like:

```js
// Without JSX
let helloWorld = React.createElement('div', null, 'Hello World!');

// Using JSX
let helloWorld = <div>Hello World!</div>;

// Both produce a JS object that looks something like this...
let helloWorld = {
  key: null,
  props: {
    children: 'Hello World!',
  },
  ref: null,
  type: 'div',
};
```

---

class: center, middle

### JSX?

JSX is an XML syntax that can be used to construct the markup in React components.

JSX makes it **easier to read and write** React components in our code, but React does work without JSX too.

---

class: center, middle

.large[
Let's take a closer look at how we would create a React component both ways...
]

---

# Hello World: No JSX

Without JSX...

```html
<div id="root"></div>
```

```js
import React, { Component } from 'react';
import ReactDOM from 'react-dom';

class App extends Component {
  render() {
    return (
      ￼￼￼￼React.createElement('h1', {id: 'title'}, 'Hello, world!')
    );
  }
}

ReactDOM.render(
   React.createElement(App, null),
   document.getElementById('root')
);
```

---

# Hello World: JSX

With JSX now...

```html
<div id="root"></div>
```

```js
import React, { Component } from 'react';
import ReactDOM from 'react-dom';

class App extends Component {
  render() {
    return <h1 id="title">Hello, world!</h1>;
  }
}

ReactDOM.render(<App />, document.getElementById('root'));
```

_More readable, less typing!_

---

# Other Things to Note

- We must import the `React` and `ReactDOM` libraries before we can create React components
- `React` provides us with a `Component` class to extend and create our own components (we can also create _functional stateless components_ without the `Component` class)
- `render` method comes from `Component`, and is required
- If you want to return React elements on more than one line, you must wrap your return value in `()`
- Look ma, no quotes! (...because JSX isn't a string)

---

# JSX Gotchas

- There must be **exactly one outer-most element returned** with your JSX (so you can't return sibling elements, only a parent with children)
- To add a comment in JSX use: `{/* a comment */}`
- If you need to add a `class` to an element, you must use `className`
- If you need to add a `for` attribute, you must use `htmlFor`

_Continued..._

---

# More JSX Gotchas

- Self-closing tags must have a `/` before the `>`
- Event listener names must be camel case (e.g. `onClick`)
- JSX must be transformed into real JS to be parsed by ES5 JS engines (we'll use Babel for that)

---

# Exercise 2

Your turn! Time to create your first React component...

Open a Codepen and try creating a React Component that simply adds the "So Much To Do" `<h1>` to an app.

Note that in Codepen, you don't explicitly import `React` or `ReactDOM`, but you will need to go to the Settings tab in the JS panel to "Quick-add" these libraries to your pen.

---

# The Virtual DOM

- The virtual DOM is an **in-memory representation of real DOM elements** generated by React components before any changes are made to the page
- It exists on the top of the DOM or some other render target
- When changes are made to the virtual DOM, React figures out the best way to **batch those changes** to the underlying DOM structure

---

class: center, middle

.inline-images[
![Virtual DOM Diff](/public/img/slide-assets/virtual-dom-diff.png)
]

---

class: center, middle

.large[
[Or this diagram...](https://bogdan-lyashenko.github.io/Under-the-hood-ReactJS/stack/book/Intro.html)
]

---

# Why This Matters

- The DOM wasn't designed for creating dynamic UIs
- Web apps exist so that users can interact with them in a task-oriented way&mdash;this means that users can/will influence the state of the app, and we need some way to render those changes to the DOM
- The virtual DOM helps with performance in this regard (versus directly manipulating the DOM)

---

template: inverse

# Creating a React App

---

class: center, middle

<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">Marc was almost ready to implement his &quot;hello world&quot; React app <a href="https://t.co/ptdg4yteF1">pic.twitter.com/ptdg4yteF1</a></p>&mdash; Thomas Fuchs (@thomasfuchs) <a href="https://twitter.com/thomasfuchs/status/708675139253174273">March 12, 2016</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

---

class: center, middle

.large[
Some initial steps...
]

---

# Software Installation

Facebook makes it easy to configure a build set-up for a basic React app with their **[Create React App](https://github.com/facebookincubator/create-react-app)**. To install it globally on your system, run:

`npm install -g create-react-app`

We'll also want to install the **[React Developer Tools for Chrome](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi?hl=en)** to assist with debugging.

---

# ToDo App Set-up

In the exercises that follow, we're going to create a basic to-do app using React. To create you app, run the following command in an appropriate directory:

`create-react-app react-todo`

Now `cd` into your `react-todo` directory, and run:

`npm start`

You should now be able to access the app on **http://localhost:3000**.

---

# What We Have Now

A boilerplate React app with:

- Babel transpiling (so we can use ES2015 and JSX)
- Webpack for bundling
- A development server

_All with zero configuration!!_

---

template: inverse

# Working with Components

---

# Conditional Rendering

Sometimes we need to conditionally render content in a component:

```js
render() {
  let hello = true;

  return (
    <div>
      <h1>Awesome App</h1>
      { hello &&
        <p>Hello, world!</p>
      }
    </div>
  );
}
```

---

# Conditional Rendering

Or with if-else:

```js
render() {
  let hello = true;

  return (
    <div>
      <h1>Awesome App</h1>
      { hello ? (
        <p>Hello, world!</p>
      ) : (
        <p>Goodbye, world!</p>
      )}
    </div>
  );
}
```

---

# Conditional Rendering

We can be more verbose for clarity:

```js
render() {
  let hello = true;
  let greeting = null;

  if ( hello ) {
    greeting = <p>Hello, world!</p>;
  } else {
    greeting = <p>Goodbye, world!</p>;
  }

  return (
    <div>
      <h1>Awesome App</h1>
      { greeting }
    </div>
  );
}
```

---

# Conditional Rendering

This is a bit more compact:

```js
render() {
  let hello = true;

  return (
    <div>
      <h1>Awesome App</h1>
      <p>{ hello ? 'Hello, world!' : 'Goodbye, world!' }</p>
    </div>
  );
}
```

---

# Conditional Rendering

React components can also use switch statements:

```js
render() {
  let myValue = 2;

  switch( myValue ) {
    case 1:
      return <div>Only one</div>;
    case 2:
      return <div>More than one</div>;
    default:
      return null;
  }
}
```

Returning `null` tells the component not to render.

---

# Iterating Over Arrays

We will often want to create components that display data by iterating over a list of array items. This is easy to do in React using JS' built-in `.map()` method and an arrow function:

```js
class App extends Component {
  render() {
    const skills = ['React', 'Angular 2', 'Vue.js'];

    return (
      <ul>
        {skills.map((skill, i) => (
          <li key={i}>{skill}</li>
        ))}
      </ul>
    );
  }
}
```

Notice the use of `{}` to wrap JS expressions inside JSX.

---

# Iterating Over Arrays

Wondering what's up with the `key` attribute on the `<li>`?

The `key` attribute helps React keep track of **dynamic children** (i.e. where child items may be added, removed, re-sorted, etc.).

Even if your children aren't going to change in any way, **React will complain** to you in the browser console if you don't add a unique `key` for each item.

**Note:** Using the array item's **index is not ideal** (because these can change), so other unique values should be used for keys if possible.

---

# Exercise 3

Open `App.js` in your React app and delete the default content in the `render()`.

In its place, set up an array as a constant called `todos` and add 'Learn React' as the only item.

Next, use what you just learned about `.map()` and iterating over arrays in a component to list the to-do array item inside an unordered list element.

You can also remove the default logo `import` and delete the file too.

---

# Types of Components

There are two way we will create components:

1.  Using ES2015 classes
2.  Using stateless functions

---

# ES2015 Class

We've already seen an example of a React component built using an ES2015 class:

```js
class App extends Component {
  render() {
    return <h1 id="title">Hello, world!</h1>;
  }
}
```

---

# Stateless Function

In more recent versions of React, we can also build components using this syntax:

```js
const App = () => {
  return <h1 id="title">Hello, world!</h1>;
};

// Or more succinctly...
const App = () => <h1 id="title">Hello, world!</h1>;
```

---

# What's the Diff?

- Stateless functional components allow us to create components that are meant to be **pure functions of their props** (more on props in a moment!)
- They **do not retain internal state**
- They do not have the **component lifecycle methods** (i.e. no `render()`, etc.)
- Later this week we will use ES2015 classes to create **Container Components** and the stateless functional approach to create **Presentational Components**...

---

# Naming Components

When naming components, the convention is to use **PascalCase**. We also want to make sure we name our components in a way that makes sense given the larger context of our app.

The key is to **be descriptive**, and start with a **base noun** so components can be easily categorized. For example:

```js
<PostsContainer />  ->  <Posts />
<Posts />           ->  <PostList />, <Post />
<Post />            ->  <PostListItem />, <PostDetails/>
```

---

# Exercise 4

Add CSS to your app by copying the styles from **[the files in this gist](https://gist.github.com/mandiwise/d6c9cb0a6e9edc20e24b6cd973cdb6d7)**, clearing out the default styles in `App.css` and `index.css`, and pasting the copied styles respectively. Also wrap the `<ul>` in a `<div>` with a class of `todo-list` (remember how to treat class attributes in React).

Finally, create a stateless functional component called `ToDo` and move your list item into it, then call `.map()` on the new `<ToDo>` component instead.

Be sure to move the `key` attribute from your `<li>` onto the `<ToDo />` inside the `.map()` function. Your app will be broken now but we'll find out why in a minute!

---

# What We've Learned

- What React is
- How to use it in a project and how to use the "Create React App" tool
- What JSX and the Virtual DOM are
- How to create React components

---

template: inverse

# Questions?

{% endhighlight %}
