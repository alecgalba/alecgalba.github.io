---
layout: post
title:      "Async Actions and Promises"
date:       2018-01-04 14:22:53 +0000
permalink:  async_actions_and_promises
---


Something that tripped me up during my final project review was asynchronous actions and fulfilling promises in React. I’d like to review the problem that I was given, the difficulties it presented me at the moment, and how I have come to better understand this fundamental part of interactive applications. For context, my application is a SPA that allows users to log their dreams and order them by “likes” on the page. 

During the review I was challenged to add a button to the existing application that would log the entire data set to the console. In order to achieve this I wrote a fetch “GET” request that queried my Rails API to return all of the existing dreams in JSON format. I then simply console.log()-ed them and caught any errors. That went over without a hitch. Below is the code:

```
  callApi = () => {
    const API_URL = process.env.REACT_APP_API_URL;
     fetch(`${API_URL}/dreams`, {
      method: "GET",
    })
    .then(res => {
      return res.json()})
    .then(dreams => console.log(dreams))
    .catch(err => console.log(err))
  }

```

And of course, here is the button that was attached to the DreamCard component: 

```
<button onClick={this.callApi}>Call Api</button>
```

My instructor then challenged me by adding four simple lines that, at first, seriously confused me and tripped me up. I think the primary reason for my confusion came with the unusual format of the function when these lines were added. Here is the new code with the devious four lines:

```
  callApi = () => {
    console.log('a')
    const API_URL = process.env.REACT_APP_API_URL;
     fetch(`${API_URL}/dreams`, {
      method: "GET",
    })
    .then(res => {
      console.log('b')
      return res.json()})
    .then(dreams => console.log('c',dreams))
    .catch(err => console.log('d', err))
    console.log('e')
  }

```

Notice the difference? Previously I had never really had to think about the order in which the data was being output to the console because of my simple API and minimal lag time between fetching and fulfilling requests. These differences were down to milliseconds and I never considered extreme situations where lag time could be greater or what is being output when. This example helped me to understand these nuances and I think made me understand this concept with much greater depth.

My instructor asked me to predict the order in which “a”, “b”,  “c”,  “d”, and “e” would be outputted in the console. Can you tell before I give away the answer? If so, great job! If not, that’s ok! We are all still learning.

Before I give the answer, let’s talk a bit about what fetch() does and what promises are in React and JavaScript.

When we use the fetch() function, it inherently creates a Promise as a filler point for the data that is being recalled. If Promises did not exist, we would see lines of code running with a response that we cannot work with due to a lack of data. Promises are objects that represent some data values that would be made available after a fetch request resolves. While the promise is waiting to be resolved we can send an action that places our application in a “loading state”. Once the Promise is resolved we have access to the returned data by chaining on a then() function in the action. The then() function is then able to parse the data into usable JSON format and we can do what we want with it.

These steps are best completed by the use of middleware in order to dispatch the loading, request, and response actions in the appropriate order. In this case I used Redux Thunk. You can read more about Redux Thunk Middleware [here](https://github.com/gaearon/redux-thunk).

Ok, back to our solution.  I'll save you some scolling and show the action again: 

```
  callApi = () => {
    console.log('a')
    const API_URL = process.env.REACT_APP_API_URL;
     fetch(`${API_URL}/dreams`, {
      method: "GET",
    })
    .then(res => {
      console.log('b')
      return res.json()})
    .then(dreams => console.log('c',dreams))
    .catch(err => console.log('d', err))
    console.log('e')
  }

```

If you guessed the order would be “a”, “b”, and then “c”, “e”…you and I were both wrong. Like I said before, I had never really had to consider the minute differences of when my asynchronous actions were resolved due to their seemingly fast performance. However, let that not deceive you!

The correct order of output is “a”, “e”, “b”, and finally “c”. This is due to the Promise not yet being resolved!

As we can see, the “b” and “c” are dependant on the Promise being resolved by the fetch() request and won’t be logged in the console until that action is resolved. Meanwhile, the “a” is the first to be logged due to its placement at the top of the function and “e” is logged second due to it not being weighed down by the request. That means “b” and “c” are run sequentially because “c” is dependant on “b” being resolved before it can be resolved itself. 

And if you’re worried about “d”, there are no errors in this function so we will never see it. Sorry “d”!

![Dee gif](https://media.giphy.com/media/KtMao0S8DyTpS/giphy.gif)

I hope this post can help someone better understand this concept as much as it did for me. For additional reading on these concepts see the links below.

[Async.JS and Promises](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function) 


[A great post on using Redux](https://codepen.io/stowball/post/a-dummy-s-guide-to-redux-and-thunk-in-react) 

Onwards!



