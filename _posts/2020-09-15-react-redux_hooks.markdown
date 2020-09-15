---
layout: post
title:      "React-Redux Hooks"
date:       2020-09-15 23:06:39 +0000
permalink:  react-redux_hooks
---


Today I want to talk about React-Redux Hooks and how we can use them. Redux support for React Hooks was introduced with the release of React-Redux version 7.1, which provides two very helpful hooks: useSelector() and useDispatch(). 

The cool thing about Hooks is that they are really just functions. In a React-Redux app we can use hooks as an alternative to using the connect() higher order component when we need to access the Redux store in a component. So how do we use this?

You'll still need to wrap the entire app in a `<Provider>` component in the index.js file. Everything on the Redux side will stay the same. Whats different is how you set up your React components in order to access the store. 

With these fancy new hooks there is no longer a need to wrap components in `connect(mapStateToProps, mapDisaptchToProps)`. Lets see how we can rewrite a component to use React-Redux Hooks instead of connect()

Below you can see an example of a component that is using connect to access the Redux store. 

```
export const Count = ({ count, addCount }) => {
  return (
    <main>
      <div>Count: {count}</div>
      <button onClick={addCount}>Add to count</button>
    </main>
  );
};

const mapStateToProps = state => ({
  count: state.counter.count
});

const mapDispatchToProps = { addCount };

export default connect(mapStateToProps, mapDispatchToProps)(Count);
```

Ahh the classic counter example. So exciting. Okay now lets see what changes when we do it the Hooks way...

```
import React from "react";
import { useDispatch, useSelector } from "react-redux";
import { addCount } from "./store/counter/actions";

export const Count = () => {
  const count = useSelector(state => state.counter.count);
  const dispatch = useDispatch();

  return (
    <main>
      <div>Count: {count}</div>
      <button onClick={() => dispatch(addCount())}>Add to count</button>
    </main>
  );
};
```

Okay! So we went from 21 lines of code to 17 and everybody loves to type less. But whats going on here?

Well the truth is nothing new is going on with this new setup. The useSelector() is basically mapStateToProps. For useSelector() you pass in a function that takes in the redux state and it returns whichever part of state the componenent needs, so in this example the component needs to know what number the counter is at. Its important to be aware that useSelector() uses strict object reference equality ( === ) as opposed to connect(), which uses shallow equality checks in order to decide if its time to re-render. One way to deal with this is to call useSelector() multiple times if a component needs multiple pieces of state instead of returning all of those pieces in a single object. This will make sure that you don't have any unnecessary re-rendering. The selector will run whenever the function component renders or whenever an action is dispatched. After the action is dispatched the selector will check if the previous selector result value is different from the current result value and if so it will trigger a re-render. Going back to the thrilling counter example: I push a button, that dispatches addCount which increases the value of count by one and since an action has been dispatched the selector will perform its comparison, the change will be noticed and the component will re-render. Boom. 

The other hook helping us out is useDispatch, which is basically the slimmer version of mapDispatchToProps. This hook returns the dispatch function which allows components to dispatch actions. Easy! So, by combining our super cool hooks we are able to access everything in the Redux store.   

And then there is of course the question of why. Why this change? Why change from the connect() approach to hooks? Well you certainly don't have to, React has firmly stated that it won't be removing class components. But using hooks does create cleaner code by reducing the need to wrap components in other components and Providers and Routers (also referred to as "wrapper hell"). It makes the code conceptually less complex which may make it a more enjoyable coding experience. But ultimately both methods can be used for the purpose of accessing the Redux store and both methods are perfectly valid. 
