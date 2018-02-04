---
layout: post
title:      "A Recursion Excursion"
date:       2018-02-04 14:46:20 +0000
permalink:  a_recursion_excursion
---


Today we are going to be talking about recursion. We will be discussing what recursion is, how to do it, and why it is useful.

> Recursion is when a function calls itself until it doesn’t. 

That’s it. 

A lot of people think recursion is hard because we often see a first example of recursion through the use of a Fibonacci sequence algorithm. I believe that this makes the concept difficult to understand for beginners because there is no real usefulness for the Fibonacci sequence in everyday programming.

So, if you see someone using the Fibonacci sequence as an example after you read this post…put both of your fingers in your ears and kick them in the shins. For me.

We will not be doing that here. Instead, we will be begin by using a much simpler example by implementing a countDownFrom() function using recursion. This function will have the ability to count down from any arugument given it, assuming it is a number. Then we will move on to something that you might find as a real world problem in structuring data with recursion.

Let’s quickly write the outline of the countDownFrom() function as if we had no idea what recursion is or how to implement it. In other words, let’s write this function as if you were me 6 months ago.

```
let countDownFrom = (num) => {
	Console.log(num)
	countDownFrom(num – 1)
}

countDownFrom(10)

```

What do you think this is going to output? Six months ago, I would have said that we should see the numbers 10-0 printed to the console in descending order. But I would have been wrong. In fact this function is going to create a stack overflow and show us two important concepts when it comes to utilizing recursion in your code.

First , this function, as written above, is going to eventually print out the error “Maximum call stack size exceeded.” The call stack is the stack of function calls that your code has made. In most non-functional programming languages, there is an upper limit of how many call you can make to your stack before seeing this error. Since call stacks are executed in a LIFO (last in, first out) order, making too many calls to a call stack will produce a “tail” of function calls which may overload your call stack and produce this error. Luckily since ECMAScript6 JavaScript supports something called tail call optimization and can mitigate the production of this error.

However, in order to ensure that you will never see this error again (I hope) you should remember our second concept – the base case! Think of the base case as a stopping point for your function. We will now include a base case to our example.
```
let countDownFrom = (num) => {
	if (num === 0) return;
	console.log(num)
	countDownFrom(num – 1)
}

countDownFrom(10)

```
And there it is! Our output shows 10-1 in descending order in our console. We just wrote our first JavaScript function using recursion! 

While base cases are important to remember when writing recursive functions, it is also important to remember that sometimes a function might not need a base case. This may be when working with data from a database that has a finite amount of data points.

If you are now asking yourself, but why did we use an unknown concept like recursion when we could have just used a familiar “for” or “while” loop, that’s great! We could have certainly achieved the same output with a loop and for something as simple as this, perhaps it may even make more sense.

A small pro-tip: every time you write a loop, you can use recursion instead. However, every time you use recursion, you might not be able to use a loop.

Let’s look at a bit more complex of an example next to demonstrate this idea. We are going to use my favorite sport and league as an example.

Imagine we have a relational database that details the two teams and their top players in La Liga Santander, the Spanish football top flight league. We are going to write a recursive function that creates a tree structure out of the mock database for easy readability. Here is our database.
```
let football = [
	{ id: 'UEFA', 'parent': null },
	{ id: 'La Liga', 'parent': 'UEFA' },
	{ id: 'Barcelona', 'parent': 'La Liga' },
	{ id: 'Real Madrid', 'parent': 'La Liga' },
	{ id: 'Lionel Messi', 'parent': 'Barcelona' },
	{ id: 'Andres Iniesta', 'parent': 'Barcelona' },
	{ id: 'Gerard Pique', 'parent': 'Barcelona' },
	{ id: 'Cristiano Ronaldo', 'parent': 'Real Madrid' },
	{ id: 'Luka Modric', 'parent': 'Real Madrid' },
	{ id: 'Sergio Ramos', 'parent': 'Real Madrid' }
];

```
So as we can see we have “UEFA” at the top of our tree structure with its parent value set to null. The  parent node of this tree has one child with “La Liga” as its ‘id’. Then we have two children values in “Barcelona” and “Real Madrid” each with three children of their own, some of the most famous footballers on earth. 

Our goal is to create an output that looks something like the following.
```
{
  "UEFA": {
    "La Liga": {
      "Barcelona": {
        "Lionel Messi": {},
        "Andres Iniesta": {},
        "Gerard Pique": {}
      },
      "Real Madrid": {
        "Cristiano Ronaldo": {},
        "Luka Modric": {},
        "Sergio Ramos": {}
      }
    }
  }
}
```
We are going to call our function “makeTree()” to make this easy. First off we are going to use our database name as our first argument and use the ‘parent’ key as our second argument, which will be our point of reference for extracting and categorizing the desired data. Then we are going to initiate a variable called “node” that is going to represent each, well, node of our tree. Here it is to start us off with the function call below it.
```
let makeTree = (football, parent) => {
	let node = {};
	return node
}

console.log(makeTree(football, null))
```
Next we are going to want to filter our original database for the information that we are looking for. We can use the filter() method for this! Let’s filter for the root element like so:
```
football.filter( x => x.parent === parent )
```
Ok now this is going to produce an array that only contains the parent of 'null' due to our function call in the console.log(). What we then want to do is call the makeTree() function recursively on each child element to assign the data correctly. We can use the forEach() function for this!
```
.forEach( y => node[y.id] = makeTree(football, y.id))
```
Here we are assigning each id to the empty node object and that is going to get a subtree. This subtree is created by recursively calling the makeTree() function so we will then have a full blown recursive function. The stark contrast is that we are now setting the ‘id’ of each subtree as the second argument of our makeTree() function. This is how we are going to gain our structure for our final output. Let’s put it all together.
```
let makeTree = (football, parent) => {
	let node = {};
	football
	   .filter( x => x.parent === parent )
	   .forEach( y => node[y.id] = makeTree(football, y.id))
	
	return node
}

console.log(makeTree(football, null))
```
If you followed along and entered the function as above you will notice that the output is not exactly what we want. But rest assured, it is correct. To prove that, we need to JSON.stringify() our output to make it legible. Here is the revised “stringified” version.
```
let makeTree = (football, parent) => {
	let node = {};
	football
    .filter( x => x.parent === parent )
    .forEach( y => node[y.id] = makeTree(football, y.id))
		
	return node
}

console.log(
   JSON.stringify(
      makeTree(football, null)
   , null, 2)
)
```
I will not go into how the arguments in JSON.stringify() work or why they are there as it is out of scope of this piece but I suggest you look into this function as you will most likely be seeing it down the road.

Let’s break down what just happened to produce our output. In the first loop we call makeTree() by passing in categories and filtering for the data that match our second argument for the parent, which is “null”. Once we establish that we only have one (‘UEFA’), we then move on to our forEach() function call where we set the value of the id to the return value of our makeTree() function. A major change happened here, however, in that we are assigning the second argument (parent) the value of the previous id. By doing this, we are making our function traverse the database and assign the values as we want by passing in different values to the second argument until we run out of data in our database.

Phew!

To wrap this all up I would like you to check out a few resources that I have put together to further your knowledge of recursion in software engineering. I hope you enjoyed this piece on recursion and use it to perhaps write your own piece in order to make this blog post somewhat recursive! Ok that’s it for now.

Onwards!

1. [Brandon Morelli of CodeBurst on Recursion](https://codeburst.io/learn-and-understand-recursion-in-javascript-b588218e87ea)
2. [The Coding Delight - A long post on recursion, very in depth](https://www.thecodingdelight.com/understanding-recursion-javascript/)
3. [David Green of SitePoint on Recursion in Functional JavaScript]https://www.sitepoint.com/recursion-functional-javascript/)
4. And of course the CS track on Learn is a great starting point!
