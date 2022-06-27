---
title: "JestReact"
date: 2022-06-07
lastmod: 2022-06-07
draft: false
blog_tags: ["react"]
summary: " "
status: "react"
---
 
# Intro:  Here we practice some React Testing library ([Cheatsheet](https://testing-library.com/docs/dom-testing-library/cheatsheet/))

</br>
</br>
</br>

***

[Jest](https://jestjs.io/), 
 is a delightful JavaScript Testing Framework with a focus on simplicity.

It works with projects using: Babel, TypeScript, Node, [React](https://reactjs.org/), Angular, Vue and more!

</br>
</br>

## Addition Tuterial links :

[Testing-react](https://academind.com/tutorials/testing-react-apps) & this 
[Playlist](https://www.youtube.com/watch?v=YQLn7ycfzEo).

***

</br>

## Some Definitions & Examples :

***

</br>
</br>

1- **UseState** : 

- If you used classes in React before, this code should look familiar:

```javascript

class Example extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      count: 0
    };
  }

  render() {
    return (
      <div>
        <p>You clicked {this.state.count} times</p>
        <button onClick={() => this.setState({ count: this.state.count + 1 })}>
          Click me
        </button>
      </div>
    );
  }
}


```

- Hooks :

As a reminder, function components in React look like this:

```javascript

const Example = (props) => {
  // You can use Hooks here!
  return <div />;
}

```

or this :

```javascript

function Example(props) {
  // You can use Hooks here!
  return <div />;
}


```

**Hooks don’t work inside classes. But you can use them instead of writing classes.**


## What is Hook ?

Our new example starts by importing the useState Hook from React:

```javascript

import React, { useState } from 'react';

function Example() {
  // ...
}


```

**What is a Hook?** A Hook is a special function that lets you “hook into” React features. For example, useState is a Hook that lets you add React state to function components. We’ll learn other Hooks later.

**When would I use a Hook?** If you write a function component and realize you need to add some state to it, previously you had to convert it to a class. Now you can use a Hook inside the existing function component. We’re going to do that right now!


### Declaring a State Var :

*In a class*, we initialize the `count` state to `0` by setting `this.state` to `{ count: 0 }` in the constructor:

```javascript

class Example extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      count: 0
    };
  }

}
```

In a function component, we have no `this`, so we can’t assign or read `this.state`. Instead, we call the `useState` Hook directly inside our component:

```javascript

import React, { useState } from 'react';

function Example() {
  // Declare a new state variable, which we'll call "count"
  const [count, setCount] = useState(0);
}

```

### Reading State :

When we want to display the current count in a class, we read `this.state.count`:

```html

  <p>You clicked {this.state.count} times</p>

```

In a function, we can use `count` directly:

```html
  <p>You clicked {count} times</p>


```

### Updating State :

In a class, we need to call `this.setState()` to update the `count` state:

```jsx 

  <button onClick={() => this.setState({ count: this.state.count + 1 })}>
    Click me
  </button>


```

In a function, we already have `setCount` and `count` as variables so we don’t need `this`:


```jsx

  <button onClick={() => setCount(count + 1)}>
    Click me
  </button>


```

</br>
</br>

[For more about useState](https://reactjs.org/docs/hooks-state.html#recap) .

***

</br>
</br>


2- **Render** :

- Rendering Elements : Elements are the smallest building blocks of React apps.

- An element describes what you want to see on the screen:

```jsx 


const element = <h1>Hello, world</h1>;

```

> Unlike browser DOM elements, React elements are plain objects, and are cheap to create. React DOM takes care of updating the DOM to match the React elements.

</br>

- Rendering an element into the DOM :

Let’s say there is a <div> somewhere in your HTML file:

```jsx

<div id="root"></div>

```

We call this a “root” DOM node because everything inside it will be managed by React DOM.

Applications built with just React usually have a single root DOM node. If you are integrating React into an existing app, you may have as many isolated root DOM nodes as you like.

To render a React element, first pass the DOM element to [ReactDOM.createRoot()](https://reactjs.org/docs/react-dom-client.html#createroot), then pass the React element to `root.render()`:


```javascript

const root = ReactDOM.createRoot(
  document.getElementById('root')
);
const element = <h1>Hello, world</h1>;
root.render(element);


```

</br>

[Try it on CodePen](https://codepen.io/gaearon/pen/ZpvBNJ?editors=1010).

</br>

[For more About Render](https://reactjs.org/docs/rendering-elements.html#updating-the-rendered-element). 

***

</br>
</br>


3- **Screen** :

All of the queries exported by DOM Testing Library accept a `container` as the first argument. Because querying the entire `document.body` is very common, DOM Testing Library also exports a `screen` object which has every query that is pre-bound to `document.body` (using the `within` functionality). Wrappers such as React Testing Library re-export `screen` so you can use it the same way.


```javascript

import {render, screen} from '@testing-library/react'

render(
  <div>
    <label htmlFor="example">Example</label>
    <input id="example" />
  </div>,
)

const exampleInput = screen.getByLabelText('Example')

```
***

</br>
</br>

4- UserEvent & FireEvent :

- UserEvent :

`user-event` is a companion library for Testing Library that simulates user interactions by dispatching the events that would happen if the interaction took place in a browser.

While most examples with user-event are for React, the library can be used with any framework as long as there is a DOM.

### Difference to **fireEvent** :

The built-in `fireEvent` is a utility to easily dispatch events. It dispatches exactly the events you tell it to and just those - even if those exact events never had been dispatched in a real interaction in a browser.

`user-event` on the other hand dispatches the events like they would happen if a user interacted with the document. That might lead to the same events you previously dispatched per `fireEvent` directly, but it also might catch bugs that make it impossible for a user to trigger said events. This is why you should use `[user-event]`(https://ph-fritsche.github.io/blog/post/why-userevent) to test interaction with your components.


### Writing tests with **userEvent** :

We recommend to use [userEvent.setup()](https://testing-library.com/docs/user-event/setup) when rendering your component and inline that rendering and setup in your test or use a setup function. We discourage rendering or using any userEvent functions outside of the test itself - e.g. in a `before`/`after` hook - for reasons described in "Avoid Nesting When You're Testing".

</br>

```javascript

test('trigger some awesome feature when clicking the button', async () => {
  const user = userEvent.setup()
  render(<MyComponent />)

  await user.click(screen.getByRole('button', {name: /click me!/i}))

  // ...assertions...
})

```

</br>

```javascript

function setup(jsx) {
  return {
    user: userEvent.setup(),
    ...render(jsx),
  }
}

test('render with a setup function', async () => {
  const {user} = setup(<MyComponent />)
  // ...
})

```

</br>

[For more about UserEvent](https://testing-library.com/docs/ecosystem-user-event/) .


***

</br>
</br>

5- **[Jset-dom_NPM_]**(https://www.npmjs.com/package/@testing-library/jest-dom) :


***

</br>
</br>


6- **[Async Methods]**(https://testing-library.com/docs/dom-testing-library/api-async/) :

- findBy :
  `findBy` methods are a combination of `getBy` queries and `waitFor`. They accept the waitFor options as the last argument (e.g. `await screen.findByText('text', queryOptions, waitForOptions))`.

`findBy` queries work when you expect an element to appear but the change to the DOM might not happen immediately.

```javascript
const button = screen.getByRole('button', {name: 'Click Me'})
fireEvent.click(button)
await screen.findByText('Clicked once')
fireEvent.click(button)
await screen.findByText('Clicked twice')
```

- waitFor :
When in need to wait for any period of time you can use waitFor, to wait for your expectations to pass. Here's a simple example:

```javascript

// ...
// Wait until the callback does not throw an error. In this case, that means
// it'll wait until the mock function has been called once.
await waitFor(() => expect(mockAPI).toHaveBeenCalledTimes(1))
// ...

```

`waitFor` may run the callback a number of times until the timeout is reached. Note that the number of calls is constrained by the `timeout` and `interval` options.

This can be useful if you have a unit test that mocks API calls and you need to wait for your mock promises to all resolve.

If you return a promise in the `waitFor` callback (either explicitly or implicitly with `async` syntax), then the `waitFor` utility will not call your callback again until that promise rejects. This allows you to `waitFor` things that must be checked asynchronously.

The default `container` is the global `document`. Make sure the elements you wait for are descendants of `container`.

The default `interval` is `50ms`. However it will run your callback immediately before starting the intervals.

The default `timeout` is `1000ms`.

The default `onTimeout` takes the error and appends the `container`'s printed state to the error message which should hopefully make it easier to track down what caused the timeout.

The default `mutationObserverOptions` is `{subtree: true, childList: true, attributes: true, characterData: true}` which will detect additions and removals of child elements (including text nodes) in the container and any of its descendants. It will also detect attribute changes. When any of those changes occur, it will re-run the callback.

- waitForElementToBeRemoved :

To wait for the removal of element(s) from the DOM you can use waitForElementToBeRemoved. The waitForElementToBeRemoved function is a small wrapper around the waitFor utility.

The first argument must be an element, array of elements, or a callback which returns an element or array of elements.

Here is an example where the promise resolves because the element is removed:


```javascript

const el = document.querySelector('div.getOuttaHere')

waitForElementToBeRemoved(document.querySelector('div.getOuttaHere')).then(() =>
  console.log('Element no longer in DOM'),
)

el.setAttribute('data-neat', true)
// other mutations are ignored...

el.parentElement.removeChild(el)
// logs 'Element no longer in DOM'

```

</br>

`waitForElementToBeRemoved` will throw an error if the first argument is `null` or an empty array:


</br>

```javascript

waitForElementToBeRemoved(null).catch(err => console.log(err))
waitForElementToBeRemoved(queryByText(/not here/i)).catch(err =>
  console.log(err),
)
waitForElementToBeRemoved(queryAllByText(/not here/i)).catch(err =>
  console.log(err),
)
waitForElementToBeRemoved(() => getByText(/not here/i)).catch(err =>
  console.log(err),
)

// Error: The element(s) given to waitForElementToBeRemoved are already removed. waitForElementToBeRemoved requires that the element(s) exist(s) before waiting for removal.

```


The options object is forwarded to `waitFor`.


***

</br>
</br>

7- Mock Functions :

[Mock](https://jestjs.io/docs/mock-functions) functions allow you to test the links between code by erasing the actual implementation of a function, capturing calls to the function (and the parameters passed in those calls), capturing instances of constructor functions when instantiated with new, and allowing test-time configuration of return values.

There are two ways to mock functions: Either by creating a mock function to use in test code, or writing a [manual mock](https://jestjs.io/docs/manual-mocks) to override a module dependency.

- Example : 

Let's imagine we're testing an implementation of a function forEach, which invokes a callback for each item in a supplied array.

```javascript

function forEach(items, callback) {
  for (let index = 0; index < items.length; index++) {
    callback(items[index]);
  }
}


```

</br>

To test this function, we can use a mock function, and inspect the mock's state to ensure the callback is invoked as expected.

</br>

```javascript

const mockCallback = jest.fn(x => 42 + x);
forEach([0, 1], mockCallback);

// The mock function is called twice
expect(mockCallback.mock.calls.length).toBe(2);

// The first argument of the first call to the function was 0
expect(mockCallback.mock.calls[0][0]).toBe(0);

// The first argument of the second call to the function was 1
expect(mockCallback.mock.calls[1][0]).toBe(1);

// The return value of the first call to the function was 42
expect(mockCallback.mock.results[0].value).toBe(42);

```

[For more about Mock Func](https://jestjs.io/docs/mock-functions#mock-property) .


***

</br>
</br>


## Setting Up :

We’ll need to import some packages inside of our testing file:

```javascript


import React from "react";
import { ... } from "@testing-library/react";
import "@testing-library/jest-dom";  // optional
import userEvent from "@testing-library/user-event";
import TestComponent from "path-to-test-component";

```

- @testing-library/react will give us access to useful functions like render which we’ll demonstrate later on.

- @testing-library/jest-dom includes some handy custom matchers (assertive functions) like toBeInTheDocument and more. (complete list on jest-dom’s github). Jest already has a lot of matchers so this package is not compulsory to use.

- @testing-library/user-event provides the userEvent API that simulates user interactions with the webpage. Alternatively, we could import the fireEvent API from @testing-library/react.

> Note: fireEvent is an inferior counterpart to userEvent and userEvent should always be preferred in practice.

- No need to import jest since it will automatically detect test files (*.test.js or *.test.jsx).

> That’s a lot of setup. But good news! If you’re initializing your React repositories with create-react-app, then all the above packages come preinstalled and the scripts preconfigured in package.json.

</br>
</br>

## Our JS Example files :

**Code App.js :**

```javascript
// App.js

import React from 'react'

const App = () => <h1> Our first Test.</h1>;

export default App

```

</br>

**Code Button.js :**

```javascript
// Button.js

import React, { useState } from 'react'

const Button = () => {
    const [heading, setHeading] = useState("Magnificent Monkeys")
    const clickHandler = ()=>{
        setHeading("Radical Rhinos");
    }
    return (
    <div>
        <button type='button' onClick={clickHandler} > Click Me</button>
        <h1>{heading}</h1>
    </div>
  )
}

export default Button

```

</br>

**Code inputEvent.js :**

```javascript
// inputEvent.js

/* eslint-disable no-undef */
import React, {useState} from "react"
import {render} from '@testing-library/react'

function CostInput(){
    const [value,setValue] = useState('');

    const  removeDollarSign = value => (value[0] === '$' ? value.slice(1) : value),
    getReturnValue = value => ( value === '' ? '' : `$${value}`),

    handleChange = ev => {
        ev.preventDefault();
        const inputtedValue = ev.currentTarget.value;
        const noDollarSign = removeDollarSign(inputtedValue)

        if(isNaN(noDollarSign)) return;
        setValue(getReturnValue(noDollarSign));
    };

    return <input value={value} aria-label="cost-input" onChange={handleChange}/>
}


const Setup = () => {
    const utils = render(<CostInput />)
    const input = utils.getByLabelText('cost-input')

    return{
        input,
        ...utils,
    }
}

export default Setup;


```

</br>

**Code reactContext.js :**

```javascript
// reactContext.js

import React from "react";
import { render, screen} from '@testing-library/react'
import '@testing-library/jest-dom'
import {NameContext, NameProvider, NameConsumer} from '../react-context'

// Test default values by rendering a context consumer without a matching provider 

test('NameConsumer shows default value',()=>{
    render(<NameConsumer />)
    expect(screen.getByText(/^My Name Is:/)).toHaveTextContent(
        'My Name Is: Unknown',
    )
})


const CustomRender = (ui, {providerProps, ...renderOptions})=>{
    return render(
        <NameContext.Provider {...providerProps}>{ui}</NameContext.Provider>,
        renderOptions,
    )
}

test('NameConsumer shows value from provider',()=>{
    const providerProps={
        value:'CP30',
    }
    CustomRender(<NameConsumer />,{providerProps})
    expect(screen.getByText(/^My Name Is/)).toHaveTextContent('My Name Is: CP30')
})


test('NameProvider composes full name from first, last',()=>{
    const providerProps= {
        first: 'Boba',
        last: 'Fett',
    }
    CustomRender(
        <NameContext.Consumer>
            {value => <span>Receiverd: {value}</span>}
        </NameContext.Consumer>,
        {providerProps},
    )
    expect(screen.getByText(/^Received:/).textContent).toBe('Received: Boba Fett')
})


test('NameProvider/Consumer shows name of character',()=>{
    const wrapper = ({children})=>(
        <NameProvider first="Leia" last="Organa">
            {children}
        </NameProvider>
    )

    render(<NameConsumer />, {wrapper})
    expect(screen.getByText(/^My Name Is:/).textContent).toBe(
        'My Name Is: Leia Organa',
    )
})

```


*** 

</br>
</br>

## Our testing code :

</br>

**Code App:**

```javascript
// App.test.js

import App from './App';
import React from "react"
import { render } from '@testing-library/react'

describe("App component",()=>{
  it("render correct heading",()=>{
    const { getByRole } = render(<App />);
    // eslint-disable-next-line testing-library/prefer-screen-queries
    expect(getByRole('heading').textContent).toMatch(/our first test/i)
  });
});

```

</br>

**Code Appearance:** 

```javascript
// Appearance.test.js

// Sometimes you need to test that an element is present and then disappears or vice versa.

// Waiting for appearance
// If you need to wait for an element to appear, 
// the async wait utilities allow you to wait for 
// an assertion to be satisfied before proceeding. 
// The wait utilities retry until the query passes or 
// times out. The async methods return a Promise, so 
// you must always use await or .then(done) when 
// calling them.



        // 1. Using findBy Queries
test('movie title appears', async () => {
    // element is initially not present...
    // wait for appearance and return the element
    const movie = await findByText('the lion king')
  })



        //   2. Using waitFor


test('movie title appears', async () => {
   // element is initially not present...
 
   // wait for appearance inside an assertion
   await waitFor(() => {
     expect(getByText('the lion king')).toBeInTheDocument()
   })
 })
 

```

</br>

**Code Async:**

```javascript
// Async.test.js



                        //  findFor  //

// """findBy""" methods are a combination of """getBy""" queries and """waitFor""".
//  They accept the waitFor options as the last argument
//   (e.g. await screen.findByText('text', queryOptions, waitForOptions)).

import { waitFor } from "@testing-library/react"


// """findBy""" queries work when you expect an element to appear but the 
// change to the DOM might not happen immediately.



const button = screen.getByRole('button', {name: 'Click Me'})
fireEvent.click(button);
await screen.findByText('Clicked once')
fireEvent.click(button);
await screen.findByText('Clicked twice')



                        //  waitFor  //

// ...
// Wait until the callback does not throw an error. In this case, that means
// it'll wait until the mock function has been called once.
await waitFor(() => expect(mockAPI).toHaveBeenCalledTimes(1))

// ...

// The default interval is 50ms. However it will run your callback immediately before starting the intervals.

// The default timeout is 1000ms.

// The default onTimeout takes the error and appends the container's printed state to the error message which should hopefully make it easier to track down what caused the timeout.

// The default mutationObserverOptions is {subtree: true, childList: true, attributes: true, characterData: true} which will detect additions and removals of child elements (including text nodes) in the container and any of its descendants. It will also detect attribute changes. When any of those changes occur, it will re-run the callback.




                    //  waitForElementToBeRemoved


const el = document.querySelector('div.getOuttaHere')

waitForElementToBeRemoved(document.querySelector('div.getOuttaHere')).then(() =>
console.log('Element no longer in DOM'),
 )
                    
el.setAttribute('data-neat', true)
    // other mutations are ignored...
                    
el.parentElement.removeChild(el)
  // logs 'Element no longer in DOM'
                    


```

</br>

**Code Button:**

```javascript
// Button.test.js

import React from 'react'
import { render, screen } from "@testing-library/react"
import { userEvent }  from "@testing-library/user-event"
import Button from "./Button"

describe("App component",()=>{
    it("renders magnificent monkeys", ()=>{
        const { container } = render(<Button />);
        expect(container).toMatchInlineSnapshot();
    });

    it("render radical rhinos after button click",()=>{
        render(<Button />);
        const button = screen.getByRole("button",{name: "Click Me"});
        userEvent.click(button);
        expect(screen.getByRole("heading").textContent).toMatch(/radical rhinos/i)
    });
});


```

</br>

**Code disappearance:**

```javascript
// disappearance.test.js

//  // The waitForElementToBeRemoved async helper function
// uses a callback to query for the element on each
// DOM mutation and resolves to true when the element
// is removed.

import waitForElementToBeRemoved from '@testing-library/react'


test('movie title no longer present in DOM', async () => {
    // element is removed
    await waitForElementToBeRemoved(() => queryByText('the mummy'))
  })
  

//   Using MutationObserver is more efficient than polling the DOM at
//  regular intervals with waitFor.

// The waitFor async helper function retries until the wrapped function
//  stops throwing an error.
//  This can be used to assert that an element disappears from the page.

test('movie title goes away', async () => {
    // element is initially present...
    // note use of queryBy instead of getBy to return null
    // instead of throwing in the query itself
    await waitFor(() => {
      expect(queryByText('i, robot')).not.toBeInTheDocument()
    })
  })



  /////////////////////////////////////////

  //      Asserting element are not present 


  const submitbtn = screen.queryByText('submit')
  expect(submitbtn).toBeNull();   // it doesn't exist
  
  

  // The queryAll APIs version return an array of matching nodes.
  //  The length of the array can be useful for assertions after
  //   elements are added or removed from the DOM.


  const submitButtons = screen.queryAllByText('submit')
expect(submitButtons).toHaveLength(0) // expect no elements


// The jest-dom utility library provides the .toBeInTheDocument()
//  matcher, which can be used to assert that an element is in the body
//   of the document, or not. This can be more meaningful than asserting 
//   a query result is null.


import '@testing-library/jest-dom'
// use `queryBy` to avoid throwing an error with `getBy`
const submitButton = screen.queryByText('submit')
expect(submitButton).not.toBeInTheDocument()



```

</br>

**Code fireEvent:**

```javascript
// fireEvent.test.js

import {render, screen, fireEvent} from '@testing-library/react'

const Button = ({onClick, children}) => (
  <button onClick={onClick}>{children}</button>
)

test('calls onClick prop when clicked-True-', () => {
  const handleClick = jest.fn()
  render(<Button onClick={handleClick}>Click Me</Button>)
  fireEvent.click(screen.getByText(/click me/i))
  expect(handleClick).toHaveBeenCalledTimes(1)
})

test('calls onClick prop when clicked-False-', () => {
  const handleClick = jest.fn()
  render(<Button onClick={handleClick}>Click Me</Button>)
  fireEvent.click(screen.getByText(/click me/i))
  expect(handleClick).toHaveBeenCalledTimes(2)
})


```

</br>

**Code inputEvent :**

```javascript
// inputEvent.test.js


import {fireEvent} from "@testing-library/react"
import Setup from './inputEvent'

test('it should keep a $ in front of the input',()=>{
    const {input} = Setup();
    fireEvent.change(input,{target: {value: '23'}})
    expect(input.value).toBe('23');
})

test('it should keep a $ to be the input when the value is changed',()=>{
    const {input} = Setup();
    fireEvent.change(input,{target: {value: '$23.0'}})
    expect(input.value).toBe('23.0');
})

test('it should not allow letters to be inputted',()=>{
    const {input} = Setup();
    expect(input.value).toBe('');   // empty before
    fireEvent.change(input,{target: {value: 'Good Day'}})
    expect(input.value).toBe('');   // empty after
})


test('it should allow the $ to be deleted',()=>{
    const {input} = Setup();
    fireEvent.change(input,{target: {value: '23'}})
    expect(input.value).toBe('$23');  // need to make a change so React registers "" as a change
    fireEvent.change(input,{target: {value: ''}})
    expect(input.value).toBe('');
})

```

</br>
</br>

## Mock Function  Examples :

**Code MockFunc:**

```javascript
//MockFunc.test.js

// Mock functions allow you to test the links between code by erasing the actual implementation of a function, capturing calls to the function (and the parameters passed in those calls), capturing instances of constructor functions when instantiated with new, and allowing test-time configuration of return values.

// There are two ways to mock functions: Either by creating a mock function to use in test code, or writing a manual mock to override a module dependency.




// Using a mock function


const mockCallback = jest.fn(x => 42 + x);
forEach([0,1],mockCallback);

// the mock func is called twice
expect(mockCallback.mock.calls.length).toBe(2);

// the first argument of the first call to the func was 0
expect(mockCallback.mock.calls[0][0]).toBe(0);

// the first argument of the secand call to the func was 0
expect(mockCallback.mock.calls[1][0]).toBe(1);

// the return value of the first call to the func was 42
expect(mockCallback.mock.results[0].value).toBe(42);


function forEach(items, callback) {
    for (let index = 0; index < items.length; index++) {
      callback(items[index]);
    }
  }

  ////////////////////////////////////////////////////


```

</br>

**Code MockImplementation:**

```javascript
// MockImplementation.test.js

// Still, there are cases where it's useful to go 
// beyond the ability to specify return values and
// full-on replace the implementation of a mock function.
// This can be done with jest.fn or the mockImplementationOnce
// method on mock functions.

const myMockFn = jest.fn(cb => cb(null,true));

myMockFn((err, val) => console.log(val));

// > true



// foo.js

module.exports = function () {
    // some implementation;
  };
  

  
  // test.js

  jest.mock('../foo'); // this happens automatically with automocking
const foo = require('../foo');

// foo is a mock function
foo.mockImplementation(() => 42);
foo();
// > 42

// When you need to recreate a complex behavior of
//  a mock function such that multiple function
//  calls produce different results, use the 
// mockImplementationOnce method:


const myMockFn = jest
  .fn()
  .mockImplementationOnce(cb => cb(null, true))
  .mockImplementationOnce(cb => cb(null, false));

myMockFn((err, val) => console.log(val));
// > true

myMockFn((err, val) => console.log(val));
// > false


// When the mocked function runs out of
//  implementations defined with mockImplementationOnce,
//  it will execute the default implementation set
//  with jest.fn (if it is defined):

const myMockFn = jest
  .fn(() => 'default')
  .mockImplementationOnce(() => 'first call')
  .mockImplementationOnce(() => 'second call');

console.log(myMockFn(), myMockFn(), myMockFn(), myMockFn());
// > 'first call', 'second call', 'default', 'default'



// For cases where we have methods that are typically 
// chained (and thus always need to return this),
//  we have a sugary API to simplify this in the form of a 
//  .mockReturnThis() function that also sits on all  mocks:

const myObj = {
    myMethod: jest.fn().mockReturnThis(),
  };
  
  // is the same as
  
  const otherObj = {
    myMethod: jest.fn(function () {
      return this;
    }),
  };
  
 
```

</br>

**Code MockModule:**

```javascript
// MockModule.test.js


// users.js

import axios from 'axios';

class Users{
    static all(){
        return axios.get('/users.json').then(res => res.data);
    }
}

export default Users;


/////////////////////////////

// Now, in order to test this method without 
// actually hitting the API (and thus creating 
// slow and fragile tests), we can use the 
// jest.mock(...) function to automatically mock
//  the axios module.

// Once we mock the module we can provide a 
// mockResolvedValue for .get that returns the data 
// we want our test to assert against. In effect, 
// we are saying that we want axios.get('/users.json')
//  to return a fake response.

/////////////////////////////

// users.test.js

import axios from 'axios';
import Users from './users';

jest.mock('axios');

test('should fetch users', () => {
  const users = [{name: 'Bob'}];
  const resp = {data: users};
  axios.get.mockResolvedValue(resp);

  // or you could use the following depending on your use case:
  // axios.get.mockImplementation(() => Promise.resolve(resp))

  return Users.all().then(data => expect(data).toEqual(users));
});



```

</br>

**Code MockName:**

```javascript
// MockName.test.js

// You can optionally provide a name for your mock 
// functions, which will be displayed instead of 
// "jest.fn()" in the test error output. Use this if 
// you want to be able to quickly identify the mock
//  function reporting an error in your test output.


const myMockFn = jest
  .fn()
  .mockReturnValue('default')
  .mockImplementation(scalar => 42 + scalar)
  .mockName('add42');




//   Finally, in order to make it less demanding to assert
//    how mock functions have been called,
//     we've added some custom matcher functions for
//      you:

// The mock function was called at least once
expect(mockFunc).toHaveBeenCalled();

// The mock function was called at least once with the specified args
expect(mockFunc).toHaveBeenCalledWith(arg1, arg2);

// The last call to the mock function was called with the specified args
expect(mockFunc).toHaveBeenLastCalledWith(arg1, arg2);

// All calls and the name of the mock is written as a snapshot
expect(mockFunc).toMatchSnapshot();

// The mock function was called at least once
expect(mockFunc.mock.calls.length).toBeGreaterThan(0);

// The mock function was called at least once with the specified args
expect(mockFunc.mock.calls).toContainEqual([arg1, arg2]);

// The last call to the mock function was called with the specified args
expect(mockFunc.mock.calls[mockFunc.mock.calls.length - 1]).toEqual([
  arg1,
  arg2,
]);

// The first arg of the last call to the mock function was `42`
// (note that there is no sugar helper for this specific of an assertion)
expect(mockFunc.mock.calls[mockFunc.mock.calls.length - 1][0]).toBe(42);

// A snapshot will check that a mock was invoked the same number of times,
// in the same order, with the same arguments. It will also assert on the name.
expect(mockFunc.mock.calls).toEqual([[arg1, arg2]]);
expect(mockFunc.getMockName()).toBe('a mock name');

```

</br>

**Code MockProp:**

```javascript
// MockProp.test.js

  const myMock1 = jest.fn();
  const a = new myMock1();
  console.log(myMock1.mock.instances); 
// > [ <a> ]

const myMock2 = jest.fn();
const b = {};
const bound = myMock2.bind(b);
bound();
console.log(myMock2.mock.contexts);
// > [ <b> ]


```

</br>

**Code MockReturn:**

```javascript
//  MockReturn.test.js

const myMock = jest.fn();
console.log(myMock());
// > undefined

myMock.mockReturnValueOnce(10).mockReturnValueOnce('x').mockReturnValue(true);

console.log(myMock(), myMock(), myMock(), myMock());
// > 10, 'x', true, true

//////////////////////////

const filterTestFn = jest.fn();

// Make the mock return `true` for the first call,
// and `false` for the second call
filterTestFn.mockReturnValueOnce(true).mockReturnValueOnce(false);

const result = [11, 12].filter(num => filterTestFn(num));

console.log(result);
// > [11]
console.log(filterTestFn.mock.calls[0][0]); // 11
console.log(filterTestFn.mock.calls[1][0]); // 12



```