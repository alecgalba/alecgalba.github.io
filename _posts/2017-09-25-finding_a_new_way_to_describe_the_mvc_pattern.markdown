---
layout: post
title:  "Finding A New Way To Describe The MVC Pattern"
date:   2017-09-26 03:04:09 +0000
---

## Going from restaurants to the football pitch
> Mijo, this all sounds great and I'm glad you're learning something; but what the hell are you talking about?
> - My Pops

### The MVC Conundrum
So far through my current coding experience, I find myself describing what I am learning to my parents from Application Program Interfaces, Web Frameworks, HTML, CSS, Ruby, Sinatra, Rails, TCP/IP - the list keeps on growing. On many occassions I have described something that they have been able to grasp and I revel in the feeling of introducing them to concepts they have never heard of much like when they raised me and intriduced me to this complicated world.

However, one concept that they have never quite grapsed (and admittedly, one that I am still struggling to fully internalize myself) is the concept of the MVC paradigm (Model, View, Controller).

Through my research to further discover this concept, I have run into the same explanation of the MVC paradigm that you are probably familiar with if you clicked the first 10 google results for MVC. I am of course talking about the "Restaurant" analogy that is repeated ad mortem. If you are unfamiliar, a small breakdown goes as follows:
##### MVC Breakdown
* Model - The Chef. This is where the logic/brains of your application is located. It is where the data is manipulated, interpretted, and saved. In Sinatra, the models are normally written as Ruby classes and can connect to the database to persist user input.

* View - The Customers. This is the front-end of the application; what the users see and how they interact with your application. The view normally consists of HTML, CSS, ERB (Embedded Ruby), and Javascript. The customers order food (input) and communicate with the waiter(controller) through forms and links.

* Controller - The Waiter. This is the middle-man of your application; the link bewteen the models and the views. The controller relays information from the browser to the application and vice versa. They take requests from the customer to the kitchen, and take the meals from the kitchen to the customer. The controller performs this action through the use of routes (such as 'GET', 'POST', 'PATCH', and 'DELETE' to name a few)

### A New Look
I have spent many hours thinking about this pattern and I think I can understand the breakdown with relative ease now. That said, I still think about how my family, being relative technological newbies, could comprehend this paradigm in terms that they fully understand.

My family are soccer fanatics (or by it's proper name, football) so have re-worked this paradigm to fit terminology that I think they would be able to understand with ease. Below is the breakdown of how I would describe it to them.

##### The Football Breakdown
* The Model - The Playbook. The model is where all of your tactics are laid out. You build a plan for the game with specific instructions for where the players are to move, attack, and defend according to specific actions taken by the opposition (user). Within the playbook you have all of your previous game information stored (database) and can draw out information that may reflect situations that you may encounter in the coming match or you can manipulate that information accordingly.
* The View – The Players. The view is what is laid out on the pitch and what the opposition sees and reacts to. The view contains players in certain positions or formations that are dictated by the playbook (model) according to the specified game plan. These players often have various characteristics that make them the perfect fit for their positions (HTML, CSS, ERB, etc.)
* The Controller – The Coach. The controller is the brain behind what the opposition sees or reacts to and how the players perform. The coach relays information that they decipher from the playbook (model) and dictates the flow of the game through the players (views). Routes can be thought of as directions handed out by the controller (coach) according to the user’s (opposition’s) actions.

### Conclusion
Above is a small summary of one of the most fundamental parts of object oriented programming in web frameworks for building web applications – the MVC paradigm. I attempted to summarize the process in a fashion that is reflective of my knowledge and can be easily interpreted by someone who has little background with the subject material like my family.

I hope someone can use this post as a way to better understand the material or structure the information in a way that they may find useful. At the very least, here we have an alternative to that pesky restaurant analogy.

Onwards!

