---
layout: post
title:      "CSS Media Queries"
date:       2018-02-27 14:20:25 -0500
permalink:  css_media_queries
---


My mind froze up when I was asked the following question durng a recent interview: "Can you tell me a little bit about CSS media queries?" After taking a beat, I fumbled out something about the how media queries were the styling applied to various media such as audio, video, images, etc.

![](https://media.giphy.com/media/irU9BlmqEwZwc/giphy.gif)


Our curriculum in Flatiron is back-end heavy and only briefly touches on the syntax and components of HTML & CSS early in the course. Most of our front-end work is saved for the later sections on React/Redux but of course we are free to explore on our own. While I thought understanding the basic structure of a webpage should get me through any interview, I have since amended my stance.

That seems to be the funny thing about being challenged on the preconception about your knowledge. If you rest on your laurels and feel content where you are, chances are there is something else waiting to be mastered. This goes for all facets of life. As such I am determined to increase my front-end knowledge and we will begin here with CSS Media Queries.

CSS Media Queries are a useful tool that allows us to measure the device screen size to then adjust our CSS layout and content so that it best suits the devices size in order to create an optimal UX. Media queries are vital to creating the immersive applications and web pages that we are accustomed to today.

Media queries start by targeting a certain media type. These types can include screen, print, speech, or tv, with many other options [available](https://www.w3.org/TR/CSS21/media.html). While a large majority of your web applications will be targeting screen devices, it may be beneficial to target special devices such as audio-based screen readers for impaired users. Luckily we are able to target multiple devices in a single media query. Take a look at this example:

```
@media screen, speech { … }
```
Despite this being a very useful tool, these media types are very broad and might not cover specific needs for certain devices or environments. As such, we can use Media Features to more specifically target more specific attributes for our intended UI characteristics.

Media features can help to describe these specific characteristics such as when computers have microphones or if a device is being utilized in a low-light condition. We can also use media features to help characterize the primary input mechanism of a user such as touch screen, remote, or mouses. For example, this query applies a theoretical style when a users main input can hover over elements:

```
@media (hover: hover) { … }
```
Similarly, media features can all be used as range features, which can be helpful in controlling the display in maximum and minimum conditions. Such conditions can include the height and width, orientation, or resolution. However, if you set a media feature query without a specific value and as long as the feature’s value is not zero, nested styles will apply.  See [here](https://developer.mozilla.org/en-US/docs/Web/CSS/@media#Media_features) for a full list of media feature references.

With this knowledge in hand, you are probably starting to think that we can put some pretty complicated media queries together in order to catch all environments which our applications may be working in. If so, you are correct! 

We can use logical operator keywords (not, and, only, etc.) that will adjust the client side view according to potentially multiple conditions. Let’s take a look at three of these logical operators and some examples to get a better understanding of this concept.

First we will look at the “only” keyword that is specifically used to prevent older browser versions that might not support modern media queries. Since styles have rapidly updated to create our modern web experience, trying to display a web page made today on a browser created in 1999 would likely cause some display issues. Luckily we can specify media queries with the “only” keyword that will filter appropriate styles for older browsers while simultaneously not affecting modern browser’s user experience; a vital tool indeed.

Here is an example of a link element that will only display on a screen with a color screen:

```
<link rel=”stylesheet” media=”only screen and (color)” href=”cool-styles.css” />
```
Hot Tip: Using the “only” keyword is useful for preventing older browsers from applying certain styles, however you must specify an explicit media type in order for this query to be valid.

Next we will examine the “and” keyword which combines various media features with other features or media types. By combining multiple media features into a single media query, developers can be extremely specific about the layout of their styling and ensure the optimal characteristics of elements on a page. For example, we can limit the minimum width and the orientation of a screen device with the following line:

```
@media screen and (min-width: 50em) and (orientation: landscape) { … }
```
Hot Tip: The “and” operator is used for chaining multiple media features together into a single query. It requires each specific feature to return true in order for the query to run and can be used for joining media features together with media types. 

While chaining together features and types might be a best use case for many scenarios, sometimes it is necessary to explicitly negate an entire media query. This is a key point so I will repeat it below:
> The “not” operator cannot be used to negate individual feature expressions in a media query. It will negate and entire query when used.

You can think of the “not” operator as an inverter for the entire media query in question. One caveat of this rule is that it will only invert a specific media query in a comma-separated list if a media type is explicitly determined. Let’s look at an example to get a better understanding of this:
```
@media not screen and (color), print and (color) { … }
```
A good practice for determining what is being negated is by inserting parenthesis in the query. You can think of PEMDAS when determining the order in which media queries are executed when using “not”. Look at the parenthesized version of our media query below:
```
@media not (screen and (color)), print and (color) { ... }
```
I mentioned comma-separated lists above so I would like to wrap up this post by going over them briefly. As you can see in our previous example we can chain media queries together using commas to apply certain styles when a user’s device matches the specific characteristics. This helps to cut down on code length and helps to organize your styling to a greater degree. Let’s take a look at the following example:
```
@media (min-height: 680px), screen and (orientation: portrait) { … }
```
Would this query apply is the user’s device was a Smartphone in portrait mode and had a minimum viewport height of 500px? Yes! Since the second portion of our query returns true our styling would apply and the user would be very pleased with their experience!

You can think of comma-separated lists for media queries as a logical “or” operator. That means that if any portion of the list returns true, the whole query is returned. Each query in a list is treated independently from the next but they all work together to find the best possible style.

While I have only brushed the surface of the use of media queries, I think that this is good footing to stand on. If this material was as new for you as it was for me, I hope you were able to learn something productive to take with you. As always I will link some more resources for you to go down the rabbit hole of knowledge.

Onwards!

1. [W3School CSS @media Rule](https://www.w3schools.com/cssref/css3_pr_mediaquery.asp)
2. [CSSMediaQueries.com](http://cssmediaqueries.com/)
3. [Learn Curriculum CSS Media Queries](https://docs.google.com/presentation/d/1j_i5pGPB5lHbgr4fpdUDheRBv2kAeOk_yhfd1Uc2f3s/edit#slide=id.p21)



