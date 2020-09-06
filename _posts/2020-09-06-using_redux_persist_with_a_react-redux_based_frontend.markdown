---
layout: post
title:      "Using Redux Persist with a react-redux based frontend"
date:       2020-09-06 20:44:51 +0000
permalink:  using_redux_persist_with_a_react-redux_based_frontend
---


While building out the react-redux frontend of my final Flatiron project I discovered a problem. Anytime the page refreshes the redux store gets wiped. This was especially problematic for the development stage since I was constantly tweaking my code and then losing my information in state upon the page reload. 

In order to fix this I decided to implement a package called Redux Persist. Redux Persist is a library which allows the redux store to be saved to the local storage of your web browser. In order to start using Redux Persist there are a couple of things to do.

First you'll need to install dependencies:

`npm install redux-persist` OR `yarn add redux-persist`

Next, you'll need to import the required packages. These should be added into the 'index.js' file:

```
import { persistStore, persistReducer } from 'redux-persist'
import storage from 'redux-persist/lib/storage'
```

There are a lot of different storage engines that you can use with redux persist which can all be found at the github repo. I decided to go ahead with localStorage.

Now persistReducer can be used to wrap the apps root reducer (the reducer returned from the combineReducers funtion). It takes two arguments: the first is an object called persistConfig and the second will be your root reducer. The persistConfig is also something that needs to be added into your index.js file. So far you should have a chunk of code in index.js that looks something like this...

```
const persistConfig = {
  key: 'root',
  storage
}

const reducer = combineReducers({
  //insert your reducers here...
})

const persistedReducer = persistReducer(persistConfig, reducer)
```

The persistConfig requires a key and storage and there are several other config settings that can be passed in as well. Now when you create your redux store you can pass that persisted reducer in. This give redux access to the power of a persisting reducer. But we still have to make sure the store itself can persist. So we need to wrap the store in persistStore like this:

```
const store = createStore(persistedReducer)

let persistor = persistStore(store)
```

Because we're using React we will need to wrap the apps root component with PersistGate. It makes sure that the UI of your app doesn't render until redux has retrieved and saved the persisted data. So now index.js should have something along these lines:

```
ReactDOM.render(
  <Provider store={ store }>
    <Router>  
    <PersistGate loading={null} persistor={persistor}>
      <App />
    </PersistGate>
    </Router>
  </Provider>,
  document.getElementById('root')
);
```

Note that the persistor is passed in as a prop to PersistGate and store is passed in as a prop to the Provider. PersistGate also takes in a prop "loading," which can either be set to null or any react instance.

And that is everything necessary to setup a persisting state in Redux. Another cool feature, which can be added into persistConfig, is whitelisting and blacklisting. If a reducer is listed under blacklist that piece of state will not be persisted. Or you can use whitelist to tell Redux persist that there are only certain reducers that you would like to be persisted. Its worth noting that whitelist and blacklist expect a string, so you'll need to do a little bit of tweaking in your combineReducers function: 

```
const persistConfig = {
  key: 'root',
  storage,
  whitelist: ['searchResults', 'searches']
}

const reducer = combineReducers({
  //...
  searchResults: searchResults,
})
```

And thats it. Your app can now do a page refresh without losing all the information in the Redux store! Yippee!  

[Redux Persist GitHub repo](https://github.com/rt2zz/redux-persist)

