---
layout: post
title:      "Ones and Zeros. Ones and Zeros, Everywhere"
date:       2018-02-09 14:40:31 +0000
permalink:  ones_and_zeros_ones_and_zeros_everywhere
---

Continuing with my theme of introductory computer science principles, today we will be discussing the binary system that is the backbone of computer functionality. When I started my journey with web development I did not fully comprehend the binary system so I have taken it upon myself to learn how to count to ten. In doing so I have now taught myself how to convert any number to binary – and you can too!

To my surprise, the binary system is much like our decimal system in more ways than I previously understood. While I was trying to find a new definition for numbering systems in learning binary it has become apparent to me that there are more similarities than differences.

In order to illustrate this we are going to first look at the fundamentals of the decimal system, or base-ten, that we are so familiar with and compare it to the fundamentals behind the binary system, or base-two. We will then examine 0-10 in binary at face value and work to memorize it. Finally we will look at two examples of how to convert any number of your choosing to binary. Strap in, folks!

Ok first thing’s first we are going to take a look at how we count in our decimal system. If you are lucky, you probably have all ten fingers on your hands at this time. It’s pretty easy to count to ten with your fingers as you lift one up at a time: 1…2…3…4…5…6…7…8…9…10…but what happens when you get to 11?

![](https://media.giphy.com/media/3ohhwfZXnlXE0UfFjW/giphy.gif)

Well if we’re counting with our fingers, we probably just say “eleven” and move on to 12…13…and so on using one finger to represent each increase. Now what about when we write it all out?

This is where we start to get into the fundamentals of the decimal system and how we interpret it. Lets look at the number ten. 10. 1-0. What does that 1 represent? What does the 0 represent? Well the 1 represents “one” ten. The 0 represents “zero” ones. So how about 11? “One” ten and “one” ones. Similarly, the number 36 is “three” tens and “six” ones. And so we can extrapolate that all the way to 99.

When we get to 100 we repeat the same process as above, only this time we are adding another placeholder to the left of the number for “hundreds”.  “One” hundreds, “zero” tens, and “zero” ones. Simple as that!

Another way of looking at this pattern is through the base-ten scale in exponential values. In a base-ten system we have a gradual increase in placeholders for powers of ten.

> (10^0 = 1; 10^1 = 10; 10^2 = 100; 10^3 = 1000; 10^4 = 10000; etc.)

So you can see that we are just increasing the number of placeholders for each value that can be represented by the ten digits 0-9.

Once we can understand this conception of the decimal or base-ten system, it becomes slightly easier to comprehend the base-two or binary system. In the same vein, we have placeholders for values of 2. Let me represent it similarly to how I presented base-ten.

> 2^0 = 1; 2^1 = 2; 2^2 = 4; 2^3 = 8, 2^4 = 16; 2^5 = 32; 2^6 = 64; 2^7 = 128; etc.

 The primary difference between base-ten and base-two is the number of digits we have to work with. In base-ten we have 10 digits (0-9). Whereas in base-two we have significantly less digits to work with (0,1). So let’s try visualizing how we count in binary. 
 
 Ok let’s start at zero: 0. Ah, that was easy. 
 
 Ok now one: 1. This is a breeze!
 
 Uh-oh! What do we do for two? We know that we don’t have a digit that can directly represent the number two. Let’s take a page out of the base-ten system and make a placeholder to the left of the number that represents “one” 2!
 
 So that means two look like: 10. This uncanny resemblance to the number “ten” will actually help us visualize the binary system with more clarity. Remember that in decimal, “ten” just means there is “one” tens and “zero” ones. Similarly in the binary system, 10 just means “one” two and “zero” ones.
 
 Ok so let’s try three: 11. This means “one” twos and “one” ones which adds up to three! But now we are at four. 
 
 How do we represent four? By adding another placeholder! Four in binary is 100 – “one” fours, “zero” twos, and “zero” ones.
 
 So now that we understand the basic fundamentals of counting in base-two or binary systems, let’s take a look at how we represent 0-10 using only zeros and ones.
 
| Decimal | Binary |
| -------- | -------- |
| 0     | 0      |
| 1    | 1    |
| 2     | 10    |
| 3     | 11    |
| 4     | 100    |
| 5     | 101    |
| 6     | 110   |
| 7     | 111    |
| 8     | 1000    |
| 9     | 1001    |
| 10     | 1010   |

So there we have it- a full print out of 1-10 in binary. Take a few moments and read it over and over in your head until you’re seeing ones and zeros.

Now for two neat tricks to help you convert any number you want into binary and be the de facto cool guy at your next binary beginners MeetUp. For these exercises you are going to need a piece of paper and a writing utensil.

This first exercise will work for any number between 1-255. First write this sequence at the very top of your page and then choose a random number:

> 128-64-32-16-8-4-2-1

I am going to show this example with the number  219. In order to find our binary representation we are going to be subtracting the first digit on the left of our sequence (128) from our starting number (219). If it fits, we are going to mark a “1” on our piece of paper. We will then take the remainder of that number and subtract the second digit in our sequence (64) from it. If this difference produces a negative number we will mark a “0” after the one and move on to the next digit in our sequence (“32”). We will repeat this until we reach a difference of zero. Try it for yourself and then look at my solution below and compare your answers.

```
219 – 128 = 91 // it fits so we place our binary starts as : “1”
91 – 64 = 27 // it fits so our binary looks like: “11”
27 – 32 = -5 // negative number so our binary looks like: “110”
27 – 16 = 11 // it fits so our binary looks like: “1101”
11 – 8 = 3 // binary: “11011”
3 – 4 = -1 // binary: “110110”
3 – 2 = 1 // binary: “1101101”
1 – 1 = 0 // it fits so our final binary looks like: “11011011”
```
Like I said, any number between 1-255 will work with this pattern but let’s go deeper. Let’s level up with the ability to convert any number we can think of into the base-two system.

It’s actually a lot simpler than the above example in my opinion once you get some practice with it. All we will do is continually divide whatever number you come up with by two and look for a remainder until we hit one divided by two. 

Start with a new blank page and at the very top of your page put down any random number (I would keep it below 10,000 for brevity). I chose the number 5525. When I divide that number by 2 we get a remainder because it is an odd number so I mark down a (1) next to that line. We then take the whole number left over (2762) and divide that by 2 and see we have no remainder so we mark a (0).  Once we get to “1/2” then we put a one in its place because of the remainder of “0.5”. To see our final binary number you just list the 1’s and 0’s from bottom to top.

Can you continue this sequence and find the final binary number? I outline the process below.

```
5525 / 2 = 2762.5 (1)
2762 / 2 = 1381 (0)
1381 / 2 = 690.5 (1)
690 / 2 = 345 (0)
345 / 2 = 172.5 (1)
172 / 2 = 86 (0)
86 / 2 = 43 (0)
43 / 2 = 21.5 (1)
21 / 2 = 10.5 (1)
10 / 2 = 5 (0)
5 / 2 = 2.5 (1)
2 / 2 = 1 (0)
1 / 2 = 0.5 (1)

// 5525 in binary is 1010110010101.
```
Now that you are armed with these tools you can no longer be intimidated by seeing binary numbers and can even go on to convert decimal numbers into binary with just some paper and pencil.

I hope you learned something from this piece and continue to check back in to my blog for more write-ups on computer science principles and web development in general. Below are some links that helped me get started and hopefully you can get something from them too.

Onwards!

1. [WikiHow to Count in Binary](https://www.wikihow.com/Count-in-Binary)
2. [Instructables Easy Way To Count in Binary](http://www.instructables.com/id/Easy-way-to-count-in-Binary-1s-and-0s/)
3. [PurpleMath Number Bases Introduction](http://www.purplemath.com/modules/numbbase.htm)
4. [A Great Converter to Check My Solutions and Prove Me Wrong](http://coolconversion.com/math/binary-octal-hexa-decimal/)


