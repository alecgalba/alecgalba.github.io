---
layout: post
title:      "Sorting Algorithms in Software Engineering Part 1"
date:       2018-02-18 18:26:44 -0500
permalink:  sorting_algorithms_in_software_engineering
---


### Selection Sort

Today we will be looking at the practice of sorting in software development and the Big-O costs that we incur when executing these algorithms. Since this topic can be large and quickly exit the scope that we can cover in this post, I will be looking at selection sorting specifically. In Part 2 of this post I will be examining the merge sorting method. We will examine what they are, how we can translate them into code, and how to calculate the Big-O costs that accompany their execution.

Let’s go!

I think we can all agree that when things in life are sorted for us decision-making becomes less complex. The same principle applies in software development. 

For example, your favorite streaming service probably has a method for sorting the recommendations for other TV shows or movies that you would be interested in based on your viewing history and presenting them as the first options you see. It would be inefficient to show you the least likely show that you will want to view and might even prevent you from using their service again. This is where sorting can have measurable results in end user behavior.

Since we can agree on that, let’s first look at how we can go about sorting an array using the selection sort methodology.  We will use the following array as our example:

> let outtaOrder = [8, 6, 3, 2, 5, 9, 1, 4, 7]

Can you describe the steps that your brain is performing in order to sort this array? This is a critical component of solving complex problems so it is definitely something for us to work on. Think about it for a moment before proceeding with this post.

For me, I find it easiest to think about removing the smallest number present in the array and setting it aside in another empty array. Then I go back to original array and do the same thing, continuing on until I have no more numbers in the original array and only have the new array with the removed elements in order. We can call this process “finding the minimum and removing.” Lets write a function that does that for us!

First we are going to want to set three variables that will help us generate the values we need to determine the minimum element. We begin by setting the first element in the array (outtaOrder[0]) as the arbitrary “minimum” element in order to use it for comparison in our loop. Next we will set a “minimum index” at 0. We will be dynamically updating the value of these variables in our iteration loop as we attempt to find our minimum. After looping through the array to find our values, we will call the splice() method using the “minimum index” value determined by our function. Finally we will be returning our minimum value. Let’s see this in code:

```
function findMinAndRemove(array) {
   //dynamically changing values
   let minimum = array[0]; 
	 let minimumIndex = 0;

	 for( let i=0; i<array.length; i++) {
		 if(array[i] < minimum){
			 minimum = array[i];
			 minimumIndex = i;
		 }
	 }
	 array.splice(minimumIndex, 1); 
   //we use one as the second parameter (1) to indicate the number of old 
	 //array elements to remove
   return minimum;
}
```

In essence we are going through each element of the array and holding on to the smallest value. If you read [my previous post](http://alecalba.com/the_big_deal_with_big-o_time_complexities) about determining the Big-O for an algorithm you should be able to see we have to call our findMinAndRemove() function once for every element in a given array until the array is empty. This means that the findMinAndRemove() function incurs a Big-O cost of n.

Now we will be creating our selection sort function which will call the findMinAndRemove() function for every element in the array. We will be calling the findMinAndRemove() function until the length of the original array is zero after having pushed the return value of each call to a new array (we will call it “sortedArray”). Check it out below:

```
function selectionSort(array) {
	let sortedArray = [];

	while(array.length !== 0){
		sortedArray.push(findMinAndRemove(array));
	}
	return sortedArray;
}

selectionSort(outtaOder) // [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

Can you deduce what the Big-O cost is for the selectionSort() function above? Similarly to the findMinAndRemove() function, we have to perform our “while” loop n times until the original array is empty (array.length !== 0). This means if the array length equals n, we are performing this function n times!

Knowing that we have to use both of these functions in order to fulfill our desired outcome, we can see that the Big-O cost of selection sorting an unsorted array is n^2. But is there another way?

Tune in next week when we discuss the merge sort method and how it is relevant in software engineering. For now take a look through these links to gather more information on the selection sort method. If you can become familiar with this implementation and how to verbally walk yourself through the steps to solve this problem then you can pat yourself on the back. If not, no worries! Just re-read this blog post and look through the links and you should get it in no time!

Onwards!

1. [Wikipedia Selection Sort](https://en.wikipedia.org/wiki/Selection_sort)
2. [Geeks for Geeks - Selection Sort](https://www.geeksforgeeks.org/selection-sort/)
3. [Khan Academy - Analysis of Selection Sorting](https://www.khanacademy.org/computing/computer-science/algorithms/sorting-algorithms/a/analysis-of-selection-sort)

