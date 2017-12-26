---
layout: post
title:      "React/Redux Portfolio Project # 5"
date:       2017-12-26 21:14:44 +0000
permalink:  react_redux_portfolio_project_5
---


As my instructional period at Flatiron School is coming to a close and I prepare myself for a career search in a new field, I have noticed a distinct difference in the content and complete lack of lucidity in my dreams. So while I was brainstorming for my next and final project using a Rails back-end and a React/Redux front-end, I thought it would be a great benefit to have a single place where I can document these dreams. Hence, DreamState came to be.

DreamState is a fundamental CRUD (as of now actually just CRD) application that has one model, Dreams. These dreams have three attributes and the ability to store a number of “likes” by a user in order to re-arrange the presentation of these dreams on their homepage. Below are the specific requirements for the project as determined by the curriculum:

*  The code should be written in ES6 as much as possible
*  Use the create-react-app generator to start your project.
*  Follow the instructions on this repo to setup the generator: create-react-app
*  Your app should have one HTML page to render your react-redux application
*  There should be 2 container components
*  There should be 5 stateless components
*  There should be 3 routes
*  The Application must make use of react-router and proper RESTful routing
*  Use Redux middleware to respond to and modify state change
*  Make use of async actions to send data to and receive data from a server
*  Your Rails API should handle the data persistence. You should be using fetch() within your actions to GET and POST data from your API — do not use jQuery methods.
*  Your client-side application should handle the display of data with minimal data manipulation


A basic over view of the front-end structure of an application using React and Redux is as follows:
*  The Redux store dispatches actions that make API requests to the back-end
*  Redux middleware called “thunk” is utilized to turn these asynchronous requests into synchronous requests
*  A Promise is made by this action which, when resolved, dispatches a new action
*  These actions are derived by action creators in my client side application and can be used for getting and deleting elements of an application
*  Once these requests are received by a reducer a new, updated copy of the state of the element is re-rendered in the component connected to the Redux store via the react-reduc connector.
*  And repeat

While this app was challenging in its creation, I repeatedly ran into bugs with Cross Origin Resource Sharing (CORS). As I searched the web for answers to my questions, I found that this was no an issue that is secluded to my application. I discovered that this was an extremely common problem and I also found about 10 different solutions to fixing the issue. 

So today I would like to go over what CORS is and how I implemented a solution for DreamState.

Here is the error that repeatedly plagued my progress:

`Response to preflight request doesn’t pass access control check: No ‘Access-Control-Allow-Origin’ header is present on the requested resource. Origin ‘http://localhost:3000' is therefore not allowed access. The response had HTTP status code 404. If an opaque response serves your needs, set the request’s mode to ‘no-cors’ to fetch the resource with CORS disabled.`

Specifically, I ran into this problem when trying to fetch the index data of all dreams and the show data of a single dream from my Rails backend. 

First off, what is Cross Origin Resource Sharing? 

Google says: “Cross Origin Resource Sharing” (CORS) gives web servers cross domain access controls, which enables secure cross-domain data transfers.” 

I say: “It’s sort of a pain in the ass.” Go with what Google says. In all seriousness, I learned that CORS is a web server’s way of using two domain information bases and compiling them into one place, such as DreamState. CORS is common in most modern web spaces so you have probably seen it without even knowing it.

When I ran into issues with CORS, I found two solutions that would work for me. First, I could set requests mode to my back-end as “no-cors” which would return what is known as an opaque response. While I won’t go into detail about what an opaque response is, I found that is was not what I needed to complete my requests so I quickly removed that portion from my code.

The second solution I found while researching was to add “Access-Control-Allow-Origin” to the headers of my rails server responses. While I found many blogs that detailed an exact implementation of this process, I was lucky enough to find out about the “rack-cors” gem, which did all of the dirty work for me. Once I had that gem installed in my rails-api side, the error disappeared!

Slightly disappointingly so, however, further research showed that had I configured by new rails application with the “--api” flag this would have been completed for me and I probably would have never seen this error. But I think I am better off for it having to work through this issue.

[Here](https://youtu.be/Cx77Yc4w_eY) is a short walkthrough of my application.


After speaking with other students at Flatiron and some family members during the holidays, I realized that there are many features that could be added to DreamSate that could make this into a pretty cool application. Some of the ideas we generated and that I will soon be incorporating are as follows:

*  Adding users and creating “friend” relationships so people can see what their friends are dreaming about and find commonalities
*  Adding comments so users can discuss their dreams or respond to people who have had similar dreams
*  Adding search function so people can search for dreams or people
*  Adding tags to label dreams so people can search specifically by label
*  Adding share buttons so people can share DreamState across other platforms

While this application is simple right now, I think that dreams are something that we, as a community, do not discuss enough so perhaps DreamState can become a platform to kick-start a new era of dream sharing.

Onwards!

