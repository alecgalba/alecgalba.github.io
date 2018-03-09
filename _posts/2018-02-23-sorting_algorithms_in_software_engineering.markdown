---
layout: post
title:      "Sorting Algorithms in Software Engineering Part 2"
date:       2018-02-23 15:11:17 -0500
permalink:  sorting_algorithms_in_software_engineering
---

### Merge Sort

Today we are going to follow-up with last week's discussion about sorting algorithms in software engineering. You can find our discussion about selection sorting [here](http://alecalba.com/sorting_algorithms_in_software_engineering) to catch up with us. Give that a read first and then come right back!

Part 2 of our discussion will be on Merge Sorting. We will continue with our format that we set out last week where we have a brief discussion on what merge sorting is, how we can represent it in code, and the Big-O costs of implementing the merge sort method. As always I will provide links to further reading at the end of this piece for you to peruse at your leisure.

Let's go!

The Merge Sort function approaches the problem of sorting differently than Selection Sort which we called selectionSort(). When we use Merge Sort we are actually breaking down a given, unsorted array into sub-arrays that we then recursively break apart until we have a bunch of arrays with the length of 1. By definition, an array with length equal to 1 is already sorted. First we are going to have to create a merge() function and then call it recursively in our function which we will call mergeSort(). Let’s check it out.

Say that we perform our selectionSort() method on two unsorted arrays to give us two new sorted arrays. Here they are below:

```
let array1 = [1, 3, 4, 6, 8]
let array2 = [2, 5, 7, 9, 10]
```

Looking at these two arrays it is clear that we can’t just write an algorithm that alternates taking a value from one of the arrays and pushing it into a new array like we did with selectionSort(). We also can’t just add one array to the end of the other one, obviously. How would you go about describing how you can solve this problem?

We will write a merge() function that will be responsible for comparing the first index of each array (since they are already ordered and thus the first index is the minimum) and determining the minimum of that comparison. We will then make this function recursive by modifying our previously defined findMinAndRemove() function to accept two arrays and pushing the returned value to an empty array. We will be performing this recursively until one of our arrays is empty. Check this out below:

```
function findMinAndRemove(first, second) {
    //setting minimum of first and second array
	let minFirst = first[0];
	let minSecond = second[0]; 
	
	// this loop will remove the first element of an array with the smallest value
	if (minFirst < minSecond){
		return first.shift();
	} else {
		return second.shift();
	}
}

findMinAndRemove(array1, array2) // 1
```

So we have that working fine. Now let’s use that in our merge() function recursively. First we are going to want to loop through the arrays until one of the lengths is zero (remember they are already sorted) and removing the smallest value then pushing it into an empty array. Check it out below:

```
function merge(firstArray, secondArray) {
    // initializing empty array
	let sorted = [];

    // here is where we are using our findMinAndRemove() function recursively
  while(firstArray.length !== 0 && secondArray.length !== 0){
	  let currentMin = findMinAndRemove(firstArray, secondArray)
	  sorted.push(currentMin)
  }
	// we must concat both arrays together when one length reaches 0
  return sorted.concat(firstArray).concat(secondArray)
}
```

You may be looking at this last line and think to yourself: is it really necessary? While the answer is of course yes, we can visualize why by placing two console.log()’s right before we return the concat()-ed sorted array.

```
function merge(firstArray, secondArray) {
	let sorted = [];

while(firstArray.length !== 0 && secondArray.length !== 0){
	let currentMin = findMinAndRemove(firstArray, secondArray)
	sorted.push(currentMin)
}
console.log(firstArray)
console.log(secondArray)
return sorted.concat(firstArray).concat(secondArray)
}

merge(array1, array2)
// []
// [9, 10]
// [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```

To figure out the Big-O cost our the merge() function we have to determine the worst case scenario which is if we have to pass through our while loop once for every element in both arrays. Since we remove an element after each loop, we cannot exceed the sum of the length of both arrays. Thus, our Big-O cost is the sum of the length of both of our arrays. Every. Single. Time.

Hang in there for just a bit longer. It will pay off in the end.

Now we know that we can take two, unsorted arrays, and merge them into one sorted array using merge(). Therein lies the key for solving the merseSort() function complexity. To use mergeSort(), we first have to be given an unordered array of any length. Let’s create that below: 

`let toBeMerged = [7, 1, 2, 8, 6, 10, 4, 3]`

Looking at this from a high level and using the knowledge of our merge() function outlined above, how can we find a new way to sort this array? Once you have figured it out (or just continue reading below) check out the solution and compare your response.

The principle technique behind implementing mergeSort() is splitting up a given array into sub-arrays until each sub-sub-array has a length of 1. Then we will be calling the merge() function on pairs of the sub-sub-arrays, therefore merging them together recursively until we are back to one, sorted array. That’s it!

So let’s now put that into code. Remember to include the base case!

```
function mergeSort(array) {
    // here we are determining a midpoint, splitting up the given array, and initializing our sorted array
	let midpoint = array.length / 2;
	let half1 = array.slice(0, midpoint);
	let half2 = array.slice(midpoint, array.length);
	let sorted;

	if(array.length < 2) { // our base case for recursive use of merge() and mergeSort()
		return array;
	} else {
		sorted = merge(mergeSort(half1), mergeSort(half2))
	}
	return sorted
}

mergeSort(toBeMerged) // [1, 2, 3, 4, 6, 7, 8, 10]
```

Our base case dictates that we return any array unaltered if that array’s length is less than 2 (so if the length is one or an empty array). The second part of our function recursively splits the given array in half into sub-arrays (and sub-sub-arrays, etc) until we have a bunch of sub-arrays with a length of 1. The we call merge() on pairs of the sub-arrays which produces gradually larger sub-arrays until we are once again back to one sorted array.

Finally, let us now examine the Big-O cost of the mergeSort() function. What is the length of our original array (toBeMerged)?

`toBeMerged.length // 8`

So with a length of 8 if we continually split this array in half, how many levels will we go until we have eight individual arrays of the length 1? If you said 3 levels (think 2^3) then you are correct. If you remember [my Big-O blog post](http://alecalba.com/the_big_deal_with_big-o_time_complexities), you will remember that the amount of times that you divide a number (n) by 2 until you get to 1 gives you the log(n) value of a number. This means that each level that we have to divide the original array by 2 until we get arrays with lengths of 1 is n * log n. This gives us the cost of merge() within our mergeSort() function. 

Now we have to account for the sorting portion of this algorithm. As we know, the act of splitting an array in half only happens once. In our mergeSort() function we have to split the array recursively until we reach an array of length 1, thus we can deduce that we incur a cost of log n again.

To determine the final Big-O cost of the mergeSort() function we add the two costs together to get log n + n log n. Also remember that when determining the final Big-O cost we only consider the largest exponent so our final cost for the mergeSort() function is: 

> O(n log n)

This was a substantial amount of information to take in. I complied this information from multiple sources and will link these sources at the end of this piece for your perusing. If you take anything from this piece, I hope you remember that the cost of merge sorting an array is n log n. We derive that by remembering that the Big-O cost of merging is equal to the length of the two arrays combined (firstArray + secondArray = n). Then we must incur the merge operation however many times we need to split the length of the array in two to get to a length of 1 (log n). Thus we reach n log n.

Onwards!

1. [Alexander Kondov from Hacker Noon - Programming with JS: Merge Sort](https://hackernoon.com/programming-with-js-merge-sort-deb677b777c0)
2. [Benoit Vallon from Ben's Blog- The Merge Sort Algorithm](http://blog.benoitvallon.com/sorting-algorithms-in-javascript/the-merge-sort-algorithm/)
3. [Nicholas C. Zakas from NCZ Online - Computer Science in JavaScript: Merge Sort](https://www.nczonline.net/blog/2012/10/02/computer-science-and-javascript-merge-sort/)

