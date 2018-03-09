---
layout: post
title:      "Sorting Algorithms in Software Engineering Part 3"
date:       2018-03-09 16:44:35 +0000
permalink:  sorting_algorithms_in_software_engineering_part_3
---

## Insertion Sort

Today we are going to go to take a brief look at the Insertion Sort algorithm in software engineering. We will examine the principles behind its application, look at an example in code, and examine the Big-O time complexity associated with Insertion Sort. If this is your first time tuning in to my blog, I would recommend checking out the other two posts regarding [Selection Sort](http://alecalba.com/sorting_algorithms_in_software_engineering) and [Merge Sort](http://alecalba.com/sorting_algorithms_in_software_engineering) for additional sorting principles.

As always I will include a list of additional reading and watching materials for you to look over and gain additional knowledge points! Let’s go!

 As you likely could have guessed, Insertion Sort is a different way to look at how sorting works and I personally believe it to be the closest way my brain works when sorting a list of values. The easiest (and most common) way to think about Insertion Sort is to think about sorting an array of numerical playing cards.

Imagine you are at a high stakes card table in Las Vegas or your weird neighbor’s living room; whatever is more familiar for you. You have a hand of sorted cards and you are extremely keen on keeping each card that is dealt to you in precise order. The dealer can hand you one card that can potentially be higher or lower than all of the cards in your hand and can also be somewhere in the middle. Once this card is dealt, how would you begin to verbalize your thought process of placing the card in the correct position?

For me, I would start at the beginning of the cards in my hand and compare each card to the newly dealt card to compare if they were a greater value, moving one by one up the row of cards until I hit a lower value. Once I find that lower value, I would place the card in that slot. This is, at a high level, how Insertion Sort works. Let’s go a little bit deeper.

![](https://www.ppchero.com/wp-content/uploads/2017/07/inceptionweneedtogodeeper.gif)

Perhaps it would be a bit clearer to imagine this a little differently. Lets imagine that we are starting off with an unsorted array instead of an already sorted list of values. To our right, imagine this unsorted array:

```
let unsorted = [7, 10, 2, 6, 4, 9, 1, 8, 3, 5]
// very messy array
```
On our left, lets imagine an empty array.

```
let sorted = []
// very empty array
```
Insertion Sort repeatedly inserts an element from an unsorted list into a sorted order in the empty array to the left hand side. Initially we remove the first element from the unsorted array and move it into the left hand empty array. If you think about it intuitively, any array that contains only one element must be sorted by definition. So now our unsorted array and sorted array looks like this:

```
unsorted = [10, 2, 6, 4, 9, 1, 8, 3, 5]
sorted = [7]
```
We will use the first index of the unsorted array as our “next up” value that will be inserted into the sorted array in the correct order. Imagine now that we place an empty placeholder to the left of the 7 in the sorted array. We can easily compare the value of 10 vs. 7 and know that 10 is greater than 7. Therefore it is easy to see that we will have to shift the number 7 over to the empty placeholder in the sorted array and replace it with the 10. 

```
unsorted = [2, 6, 4, 9, 1, 8, 3, 5]
sorted = [7, 10]
```
Next up we have the 2 to handle. Repeat the same process of mentally inserting an empty placeholder to the left of the 7 and compare the values from left to right. Since 2 is less than both values in our sorted array, we do not have to shift any elements on this pass through and we can insert the 2 at the beginning of the array. 

```
unsorted = [6, 4, 9, 1, 8, 3, 5]
sorted = [2, 7, 10]
```
Now this is where the fun stuff starts to happens. Repeat the same process and insert an empty placeholder before the 2. Now compare the value of 6 vs. 2. Obviously 6 is greater and therefore we can shift the 2 over to the empty spot on its left and find the empty spot between the 2 and 7. Luckily 6 is both greater than 2 and less than 7 so we have found it’s place.

If you follow these steps over and over until the unsorted array is completely empty and the sorted array both contains all of our numbers while being in correct numerical order you just used Insertion Sort to sort this array!

Since we now have an understanding of how Insertion Sort works on a high level, lets look at the JavaScript code that makes it function.

So what were we doing above? Essentially we were looping through an array and comparing the values of two numbers while holding/moving an empty place value until we found the correct place to insert the “next up” value.

First lets name our function and give it a parameter of an unsorted array:

```
function insertionSort(unsortedArray) {
	//magic place
}
```
Our first priority should be to loop through the unsorted array in order to keep a copy of the element that is “next up”. Remember to start at index 1 since we are using the first number in the unsorted array as our first number in the sorted array. We can do so like this:

```
function insertionSort(unsortedArray) {
	for (let i = 1; i < unsortedArray.length; i++) {
		let placeholder =  unsortedArray[i]
	}
}
```
Great that was relatively easy. Now we have to implement looping through the sorted array and comparing it to our placeholder. If our number is larger then we are going to shift all of the elements and insert our placeholder into the correct position. We can accomplish this with a for loop within our for loop! Take a look:

```
function insertionSort(unsortedArray) {
	for (let i = 1; i < unsortedArray.length; i++) {
		let placeholder =  unsortedArray[i]
		for (var j = i - 1; j >= 0 && (unsortedArray[j] > placeholder); j--) {
			unsortedArray[j + 1] = unsortedArray[j];
		}
	}
}
```
Next up we are going to have to replace our placeholder value with the larger number in order to correctly sort our array. We can accomplish this by setting the value of the index of the largest number + 1 to the placeholder value. This is what it looks like:

```
function insertionSort(unsortedArray) {
	for (let i = 1; i < unsortedArray.length; i++) {
		let placeholder =  unsortedArray[i]
		for (var j = i - 1; j >= 0 && (unsortedArray[j] > placeholder); j--) {
			unsortedArray[j + 1] = unsortedArray[j];
		}
        unsortedArray[j + 1] = placeholder;
	}
}
```

Finally we have to return the original array which should now be sorted! Like so:

```
function insertionSort(unsortedArray) {
	for (let i = 1; i < unsortedArray.length; i++) {
		let placeholder =  unsortedArray[i]
		for (var j = i - 1; j >= 0 && (unsortedArray[j] > placeholder); j--) {
			unsortedArray[j + 1] = unsortedArray[j];
		}
        unsortedArray[j + 1] = placeholder;
	}
	return unsortedArray;
}

insertionSort(unsorted) // [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```
Very nice!

![](https://media.giphy.com/media/l0ErFafpUCQTQFMSk/giphy.gif)

In order to wrap this up, lets take a look at the best and worst case scenarios in regards to Big-O time complexity of the Insertion Sort algorithm. I have two questions for you:

> 1.	Can a call to insertionSort() cause every element in a sorted array to shift one position?
> 2.	Can a call to inserstionSort() not cause a shift in any element at all?

The answer to both of these questions is, surprisingly, yes!

Our first question would present a scenario where the value of the placeholder in our function is such that each element has to move one place over. Without going too much into the arithmetic behind this conclusion, we can imagine that the number of shifts occurs at a constant rate (c) times the number of elements (n) that we have to shift. We will have to make the shift n-1 times since we are starting from index 1 in our function. Extrapolating this out will give us a time complexity of O(n^2) which represents our worst case scenario of shifting all elements.

But what if the placeholder value is less than all of the numbers already sorted into the array? Well it would only take that number of calls to insert the value into the correct position which can be represented by O(n).

Adhering to the principles of Big-O Notation, we always say the time complexity of an algorithm is equal to the worst case scenario. As such we can confidently conclude that the Big-O time complexity of Insertion Sort is O(n^2).

I hope you enjoyed this week’s adventure into Insertion Sort. Keep an eye out for my weekly posts and remember to keep on practicing! Below are a few resources for you to go deeper into the subject of Insertion Sort.

Onwards!

1. [Insertion Sort - Algorithm Walkthrough Video by Game Constructor](https://www.youtube.com/watch?v=6K-aC_tjLrg)
2. [Insertion Sort from Khan Academy](https://www.khanacademy.org/computing/computer-science/algorithms/insertion-sort/a/insertion-sort)
3. [JavaScript Searching and Sorting Algorithms: Insertion Sort by W3Rescource](https://www.w3resource.com/javascript-exercises/searching-and-sorting-algorithm/searching-and-sorting-algorithm-exercise-4.php)

