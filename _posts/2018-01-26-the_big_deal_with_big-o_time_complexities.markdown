---
layout: post
title:      "The Big Deal with Big-O Time Complexities"
date:       2018-01-26 15:58:35 +0000
permalink:  the_big_deal_with_big-o_time_complexities
---


Computer Science principles are something that we don’t see much of in the Online Web Developer track at Flatiron School. Yet during my mock technical interview and the interviews that I have had since graduating, they are expected to be common knowledge. One major principle in CS is how well the algorithm scales as the input size increases (known as time complexities) commonly referred to as Big-O Notation.

In this post I am going to take a look at some common Big-O time complexities that you might encounter. Once again, the concept of Big-O notation is important in software development because it allows us to determine the execution time for an algorithm. This is critical for determining the most efficient solution to a problem.

Today I will be looking at four different time complexities that one may see in the wild:
* O(1) – Constant time complexity
* O(n) – Linear time complexity
* O(log n) – Logarithmic time complexity
* O(n^2) – Quadratic time complexity

Let’s go!

### O(1) – Constant Time Complexity
First we will examine the constant time complexity represented by O(1). Algorithms that execute in a constant time complexity will always take the same amount of time to complete regardless of the size of the input. Common methods that represent the O(1) time complexity include pop() and push() or when you access and element in an array; all of these examples perform one action no matter the input size.
```
	var array = [1, 2, 3, 4, 5]
	array[0] = 1
	array.pop() = 5 // array = [1, 2, 3, 4]
	array.push(5) = 5 // array = [1, 2, 3, 4, 5]

```

Think of it has having to only perform one action on the input size, no matter the size of the input. That’s it when it comes to constant time complexity. Let’s kick it up a notch!

### O(n) – Linear Time Complexity
An algorithm represents a linear time complexity when the execution time is directly proportional to the input size. This means that for large enough input sizes the running time of a given algorithm increases linearly with the size of the input. Examples of linear time complexities in software development include simple “for” loops or array methods such as indexOf(), amongst others. Check this “for“ loop out:
```
function printIt(arr) {
		for (var i = 0; i < array.length; i++) {
			console.log(array[i])
    }
}

var countries = [“Argentina”, “Belgium”, “USA”, “Mexico”]
printIt(countries) // Argentina, Belgum, USA, Mexico

```
An important aspect of O(n) is that it represents the best possible time complexity available where algorithms have to sequentially read or perform an action on its entire input.

### O(log n) – Logarithmic Time Complexity
Similar to the linear time complexity, a logarithmic time complexity occurs when the time it takes to run the algorithm is proportional to the logarithm of the input size.

I think the best way to examine this time complexity is using the twenty questions game as an example. If you are unfamiliar with the game of twenty questions, one player chooses a random number (usually within a range, if they aren’t evil) while the second player has twenty guesses to find that number. When a number is guessed, the chooser tells the guesser whether the guessed number is higher or lower than the chosen number. This helps the guesser to break down the original array of numbers into subarrays and choose accordingly from there.

We can represent this game with binary search, which also happens to be a great example of logarithmic time complexity!
```
var doSearch = function(array, targetValue) {
    var minIndex = 0;
    var maxIndex = array.length - 1;
    var currentIndex;
    var currentElement;
    
    while (minIndex <= maxIndex) {
        currentIndex = (minIndex + maxIndex) / 2 | 0;
        currentElement = array[currentIndex];
        if (currentElement < targetValue) {
            minIndex = currentIndex + 1;
        } else if (currentElement > targetValue) {
            maxIndex = currentIndex - 1;
        } else {
            return currentIndex;
        }
    }
    return -1;  //If the index of the element is not found.
};
var numbers = [11, 13, 15, 17, 19, 21, 23, 25, 27, 29, 31, 33];
doSearch(numbers, 23) //=> 6

```
Algorithms that run in logarithmic time complexity are considered highly efficient due to the fact that the ratio of the number of operations to the size of the input decreases towards zero when n increases. 

### O(n^2) – Quadratic Time Complexity
An algorithm can be described as running in quadratic time if its execution time is proportional to the square of the input size. That is, if the size of the input doubles, the number of steps quadruples. Quadratic time complexities are seen especially clearly when dealing with nested loops, bubble sorting, selection sorting, or insertion sorting. We will examine nested loops as an example here.
```
function nSquared(string, letter){
   let matches;
   for(let i = 0; i < string.length; i++){ // loop 1
      for(let i = 0; i < string.length; i++){ // loop 2...
      }
   }
}
 
nSquared("abc")

```
We can see here that the cost of loop 1 and 2 is three because of the length of the string (“abc”). This means that we are incurring a cost of 3x3, which is of course 9. Therefore we have an O(n^2) time complexity.

A top tip is that we can generally calculate the Big O of a function by counting the number of nested loops that ask us to traverse through each number. While there may be some instances where this might not be true, it is a good way to start thinking about the issue.

### Conclusion
After all of those words, maybe it might be easier to just look at a graph representing the time complexities we went over along with a couple other, higher order time complexities.

![](https://i.stack.imgur.com/jIGhf.png)

We have only just learned the surface of Big O notation and we have looked at a few of the most common examples of time complexity that you will find in software development. This post by all means did not exhaust the list of possible time complexities. You can start your search [here](https://en.wikipedia.org/wiki/Time_complexity).

One resource we have directly is the computer science track on Learn.co but I will list a few other resources that can help you get started in your own research on CS principles.

1.  [A great video explaining Big- O](https://www.youtube.com/watch?list=PLGLfVvz_LVvReUrWr94U-ZMgjYTQ538nT&time_continue=17&v=V6mKVRU1evU)
2.  [The Big-O Cheat Sheet](http://bigocheatsheet.com) by Eric Drowell
3.  [Interviewcake's Big-O explanation and a special treat of space complexity](https://www.interviewcake.com/article/java/big-o-notation-time-and-space-complexity)

Onwards!

