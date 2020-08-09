---
layout: post
title:      "Javascript Promises"
date:       2020-08-09 04:11:21 +0000
permalink:  javascript_promises
---


For project number four in my Flatiron program we were assigned to make an application with a Javascript front end and a Rails API backend. 

In order for Javascript to receive the data from the API backend we use the fetch() method, which creates something called a Promise. 

But what is a Promise? 

In Javascript a Promise is an object that represents a value that will eventually be returned, either successfully or unsuccessfully. The promise object allows us to attach callbacks as opposed to passing callbacks into the function.

In order to understand Promises its important to understand that Javascript is an asynchronous language. It doesn't strictly go from top to bottom the way a synchronous language such as Ruby would do. Javascript is multithreaded, meaning that when Javascript reaches some code that may take a while (note: in Javascript-land 1 second is considered too long) it will just continue going through the code and executing functions. When a function is wrapped inside a Promise object it has essentially become a synchronous function.

The Promise object has a state and it is said to be either pending, fulfilled, or rejected. It starts in pending and then will either become fulfilled or rejected. Once this happens the handlers in the promise's then() method are called, which is chained on the promise object. In other words the code placed inside of a promise's then statement will not run until the promise has been resolved (either fulfilled or rejected). 

The then() method takes up to two arguments: the first will be a callback function for success and the second a callback function for failure. 
Promises have another chainable method, catch(), which contains code that will run only if the promise is rejected. If no catch() method is provided to a promise and an error happens to occur there will be no error message displayed. The code will just run incorrectly without explaining itself. 

A promise guarantees us that callbacks are never run until the completion of the current event loop. The callbacks added by the then() function are also guaranteed to run regardless of whether the promise results in success or failure. Furthermore, we can make a chain of then() methods with callback functions and this chain will be run synchronously. This is because the then() statement returns a new Promise object that is different from the original. So each then() is like a step in what is known as the promise chain. 

Promises can be confusing at first glance, but there is lots of great documentation to read that can help you understand. Here are some resources that I like: 
MDN Promises: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise
MDN Using Promises: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Using_promises
Javascript Info: https://javascript.info/promise-basics
