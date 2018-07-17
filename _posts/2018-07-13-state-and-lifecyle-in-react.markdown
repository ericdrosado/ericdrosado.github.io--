<h2> Intro </h2> 
Recently I worked on some client work, and most of the stories I worked on dealt heavily with React. This was my first introduction into React. I was impressed by how React makes frontend work incredibly easy! If you are new to React, I would highly recommend doing some research to learn some of the benefits of react <a href="https://reactjs.org">here</a>. With this post, I would like to look into the state and lifecycle of a React component as well as discuss what a component is. 

<h2> React Components </h2>
React Components represent pieces of your UI. For example we might have the following:
```
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>
}
``` 
For now, do not worry about `props`, as it is simply a set of "properties" that have been defined elsewhere and can be utilized. This example is a React component. You'll notice that the return statement above looks like an HTML element, but it is actually a React element. Another important thing to note is that the tag syntax is actually JSX, which is a syntax extension to JavaScript. Also, notice the curly brace syntax, which is a special syntax to let the parser know that it needs to interpret the contents in between as JavaScript. This example above is called a "functional component." You can also use an ES6 class to define a "class component":
```
class Welcome extends React.Component {
  render() {
    return <h1>Hello, {props.name}</h1>
  } 
}
```
Both of these examples are technically equivalent. Either one can be used to achieve the same view on a users screen.

<h2> State </h2>
Now, lets get into the concept of state. For this explanation I plan on using the React tutorial example on <a href="https://reactjs.org/docs/rendering-elements.html#updating-the-rendered-element">Rendering Elements</a>. In this section a ticking clock is made with the following code:
```
function tick() {
  const element = (
    <div>
      <h1>Hello, world!</h1>
      <h2>It is {new Date().toLocaleTimeString()}.</h2>
    </div>
  );
  ReactDOM.render(
    element,
    document.getElementById('root')
  );
}

setInterval(tick, 1000);
``` 
Here we have a function called `tick` that has a constant, which represents a React element. The `ReactDom.render()` function renders the React element to the specific DOM node, in this case, `root`. You'll also notice a function called `setInterval`, which is setting how often our clock should be displayed/updated, by taking the function you would like to run as the first parameter, `tick`, and the time, in milliseconds, as the second parameter. This code will display a greeting and the time with seconds updating every second. This is fine, but it would be nice to have time as a part of State, where our clock would update automatically with React.

If you recall, we looked at two different components. We looked at a functional component and a class component. One of the benefits of using a class component is the fact that we can utilize state. So, let's take our React Element in our function, and incorporate it into a `Clock` class:
```
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }

  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}

ReactDOM.render(
  <Clock />,
  document.getElementById('root')
);
```
Let's start with the `constructor` of our class. For the constructor we are initializing `state`. This initial state is created with a date object, which we will later access for the local time.

The next section we should look at is the `render` function. This function nearly looks identical to our `tick` function from our previous example. Ultimately we are dealing with a very similar idea in that this is the React Element we want to render when the time comes.

The last section is what actually makes the call to render the view. It calls the `Clock` component and renders the React Element to the `root` DOM node.

You might have noticed that we no longer have the `setInterval` function. The code, as is, will render and display the time at the moment of rendering. This is not what we want as we would like our seconds to increment on the display. Now that we can apply the `Date()` to the state of our app, we have a way to manage the time for our app. We need to determine how to update our time in state continuously and insure that, that information is rendered.  

<h2> Lifecycle Functions </h2>
In order to utilize a component lifecycle, we'll need to use a built in function in React, `componentDidMount()`. This function will run after the component has been rendered to the DOM. This is the perfect function for us to use so we can update the time:
```
componentDidMount() {
  setInterval( 
    () => this.tick(),
    1000
  );
}
```
You might notice that we are using an anonymous function. This is so because we want to maintain the `this` binding to our current object rather than just passing the `tick` function directly as a parameter. Now, we can reintroduce `tick`, but `tick` can now set our state to the new time after every second:
```
tick() {
  this.setState({
    date: new Date()
  });
}
```
Our code should now look like the following:
```
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }

  componentDidMount() {
    setInterval(
      () => this.tick(),
      1000
    );
  }

  tick() {
    this.setState({
      date: new Date()
    });
  }

  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.
         </h2>
      </div>
    );
  }
}

ReactDOM.render(
  <Clock />,
  document.getElementById('root')
);
```
<h2> Conclusion </h2>
We should now have a fully functional "ticking" clock. We were able to introduce state as well as a lifecycle function for our state. It would be wise to "unmount" or use the `componentWillUnmount()` function so the timer will stop when `Clock` is no longer present on the DOM. It is a nice way to save resources, and ultimately a clean way to write your code.
