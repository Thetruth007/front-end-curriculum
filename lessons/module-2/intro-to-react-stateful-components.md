# Intro to Stateful React Components

In our previous lesson, we learned how to create stateless components. Stateless components are great if we just need to create html that will be be different based on what parameters/properties we pass into our component. Sometimes our components need to be able to store the information they display and change that information based on user interaction. When this is the case, you will want to use a stateful component.

## Stateful Components
Stateful components are ES6 classes that extend an abstract 'Component' class, given to us by default by React. They each have a render method that allows us to specify what should be rendered to the DOM.

In this example, we will create a counter class. This class will render a count and a button to increase the count.

```jsx
import React, { Component } from 'react';

class Counter extends Component {
  render() {
    return (
      <section>
        <span>5</span>
        <button>Add 1</button>
      </section>
    )
  }
}
```
Stateful components keep track of some sort of application data. This application data is used to determine how the component should render. As the application is used, the application data will change causing the view to change.

In our example above, the application data we will want to keep of track of is the current count.

Application data that affects how our app renders is stored in state.

## State
State is slightly different than props: state holds data that represents the actual state of our application. State is private and local to a component, whereas props are passed into a component. State can be changed and mutated through user interactions, whereas props should remain immutable.

To create state we will initialize it in our class's constructor function. Note: The super method must be called before adding state. After adding state, we can use it in our render method instead of hardcoding our count.

```jsx
import React, { Component } from 'react';

class Counter extends Component {
  constructor() {
    super();

    this.state = {
      count: 5
    }
  }

  render() {
    return (
      <section>
        <span>{this.state.count}</span>
        <button>Add 1</button>
      </section>
    )
  }
}
```

Now when we update our state, our component will rerender and display the correct count.

#### setState(newState, [callback])
The setState method is used to update the state of the application. It takes two arguments, the first is an object that represents the new state of the application. the second is an optional callback, that will be invoked after state is updated.

Let's add a method to update our state when our button is clicked.

```jsx
import React, { Component } from 'react';

class Counter extends Component {
  constructor() {
    super();

    this.state = {
      count: 5
    }
  }

  increaseCount = () => {
    const newState = {
      count: this.state.count + 1
    }

    this.setState(newState);
  }

  render() {
    return (
      <section>
        <span>{this.state.count}</span>
        <button onClick={this.increaseCount} >Add 1</button>
      </section>
    )
  }
}
```

In our example above we create our increaseCount method as an arrow function. This will insure that the keyword `this` in our function will always refer to this specific instance of our counter.

One of the more confusing things about React is when to make a component stateful. A general rule of thumb to keep in mind is that, if you're not sure if a component should be stateless or stateful, start with a stateless component. Add state if you find that you need it. Stateful components are a lot heavier than stateless component. Keep your app as lean as possible!

## Lifecycle Methods

![React Lifecycle Diagram](../../assets/images/lessons/intro-to-react-stateful-components/react-lifecycle.png)


## Conditional Rendering