---
layout: post
title:      "This Is Not The Last Time You Will Hear About ```this```"
date:       2017-12-07 16:09:14 +0000
permalink:  this_is_not_the_last_time_you_will_hear_about_this
---

Today I will be writing on what is, for me, one of the most elusive concepts of JavaScript: the keyword ```this```. My aim in this post is to provide you with the knowledge of what ```this``` is, how to use ```this```, how to figure out its scope or context, and provide examples along the way. 

 **NOTE:** The common occurrence of the word “this” is an unfortunate convention in English and makes understanding “this” concept just slightly more difficult. As such, I will be using ```this``` when referring to the JavaScript keyword and any other form of the word will be referring to the common English use. I will attempt to find other words for “this” whenever possible, but you know…English.
###  Speaking of English…
I like to think of the keyword ```this``` as being equivalent to the use of pronouns in the English language. For example, in the sentence “Alec is writing this blog post because he wanted to help others understand JavaScript.”  

Who is the word "he" referring to in the previous sentence? Alec (me), of course! 

In English, we use pronouns as a shortcut to hold the place, or value, of proper nouns. Imagine how annoying it would be to have to keep track of all of the subjects of a sentence if we didn’t have pronouns!
### How it Relates to JavaScript
Similarly in JavaScript, we use the keyword ```this``` as a shortcut to an object’s properties and their value(s). If that doesn’t make sense just yet, hang in there and check out this example:
```
var person = {
firstName: "Penelope",
lastName: "Barrymore",
showFullName: function() {
console.log(this.firstName + " " + this.lastName); // Notice how we used *this* in place of person just as we replaced Alec with he in the sentence
    }
}
person.showFullName(); // Penelope Barrymore
//Since we used "this" inside the showFullName method it will hold the value of the person object properties
```

If we were to use `person.firstName` and `person.lastName` in the `showFullName()` function in the above example then our code could potentially run into  issues with global variables of the same name, especially if we are using imported libraries. 

We need to use the keyword ```this``` to access methods and properties of the object that invokes our specific functions since we may not always know the name of the invoking object. Similar to pronouns in English, the keyword this is used as a shortcut to refer to the “antecedent object” or proper nouns in English.

When the keyword ```this``` is used inside of a method (a property of an object whose value points to a function) it equals the object that received the method call; otherwise, the keyword ```this``` is almost always referencing the global, or browser window, context. 

That concept is important so I will stylistically yell it at you: 

> **If ```this``` is referenced directly inside a method, it equals the object that received the method call. Otherwise ```this``` is referring to the global variable.**

So now we know that the keyword ```this``` can both refer to and contain the value of an object’s property and can also be considered as a shortcut to refer back to the object in context. Context is very important when using the keyword ```this``` so we will continue to explore it and explain it as we go along.
### Some ```this``` Keyword Basics in JavaScript
When functions are executed in JavaScript programs the properties are automatically assigned a value for the keyword ```this```. What that means is a variable is assigned with the value of the object that invokes the function where the keyword this is used. Confused? Don’t worry; I still am a little bit as well. That’s why I’m explaining it to you!

Another way of putting that mess of a sentence is that the keyword ```this``` always refers to and holds the value of a singular object. Therefore, it can either be used inside a function or method, as it usually is, or it can be used outside a function in the global scope, or context.

NOTE: Although we won’t explore this concept in great detail here, a small caveat exists when the program is in “strict mode”. While is “strict mode” the keyword ```this``` holds the value of “undefined” in global functions and in anonymous functions that are not bound to any object. Read more on the keyword ```this``` in strict mode [here](https://github.com/getify/You-Dont-Know-JS/blob/master/this %26 object prototypes/ch2.md#nothing-but-rules).
### Perhaps The Most Important Concept With ```this```
It took me a while to understand the implications of the following sentence but I believe that if you can remember and apply it, you can begin to understand the keyword ```this``` with proper clarity. Are you ready?

> **The keyword ```this``` is not assigned an actual value until an object invokes the function where ```this``` is defined.**

To clarify, although it might appear that the presence of the keyword ```this``` automatically assigns a value, this is not the case. In reality, to assign a value the function in which the keyword ```this``` exists must be invoked. Additionally and in almost all circumstances, the value that is assigned to ```this``` is derived by the object that invokes the function where ```this``` is present. For examples where this may not be true, see this great article by Richard Bovell [here](http://javascriptissexy.com/understand-javascripts-this-with-clarity-and-master-it/).
### Finally Some Context
Finally, we will determine how the keyword ```this``` is given context in a program, otherwise known as being applied to the call-site (or position where it is called in the call-stack). For most cases that I have come across, you can follow these three rules when determining context for the keyword ```this``` and determining its call-site (in order of precedence):

1.	Is the function called with “new”? Use the newly constructed object.
2.	Is the function called with “call”, “apply”, or “bind”? Use the explicitly specified object.
3.	Otherwise, use the global variable (or defaults to “undefined” in “strict mode”)

We will examine each of these instances a little further to wrap this all up.
### Default Binding ```this``` To The Global Variable
As we have mentioned before, the default application of the keyword ```this``` is to the global scope. Let’s first examine an example:
```
function foo() {
	console.log(this.hello); //the call-site of this is here
}

var hello = 'hello'; //global variable call

foo(); // invoking the foo function produces "hello"  from the global variable
```

We can see that the variable `var hello = ‘hello’`, is declared in the global scope and thus is synonymous with the global-object properties of the same name. We also see that when foo() is called, `this.hello` resolves to the global variable “hello” because it is a plain function reference and, since we aren’t in strict mode, will hold the value of the global variable by the same name. This is called “default binding”. 

**NOTE:** A concept closely related to default binding is “implicit binding”. Implicit binding is when a call-site uses a reference property of an object and therefore seemingly contains, or owns, the function reference at the time that the function is called. So, when there is a context object for a function reference, the “implicit binding” rule dictates that the context object should be used for the function call’s ```this``` binding. See [here](https://github.com/getify/You-Dont-Know-JS/blob/master/this %26 object prototypes/ch2.md#implicit-binding) for more info on implicit binding.
### Explicit Binding With ```this```
All functions in JavaScript have built in utilities to them via their [[Prototype]] which gives them access to the methods call() and apply(). These methods take an object as their parameter, the object to use for the keyword ```this```, and then invoke the specified function with the value of ```this```. Since we are directly stating which value of ```this``` we desire, we call this “explicit binding”. Consider this example:
```
function foo() {
	console.log(this.explicit);
}

var obj = {
	explicit: “explicitly bound this value”
};

foo.call(obj); // “explicitly bound this value”
//or
foo.apply(obj); // “explicitly bound this value”
```

When we invoke foo.call(obj) or foo.apply(obj) we are forcing it to use the value of the “explicit” variable `obj` in our use of ```this```.  While call() and apply() may differ slightly when passing in additional parameters, when it comes to binding we can just assume they are interchangeable. Perhaps another post can cover these nuances at another time.

As of ES5, we are now provided with the built-in utility of the bind() method. Below is an example of its use:
```
function foo(something) {
console.log( this.a, something );
return this.a + something;
}

var obj = {
	a: 2
};

var bar = foo.bind(obj);

var b = bar( 3 ); // 2 3
console.log( b ); // 5
```
 The bind() method returns a new function that is hard-coded to call the original function with the ```this``` context set as you defined. This convention is extremely similar to the previously mentioned call() and apply() methods, however we call this “hard-binding” due its explicit and strong characteristics. 
###  Using “new” With ```this```
The last rule we will examine for finding context when binding the keyword ```this``` is with the “new” operator. The “new” operator is a constructor in JavaScript which means that we are creating a new object, the object is prototype linked, the newly constructed object is set as the ```this``` binding for the specified function call, and is automatically returned (unless otherwise specified). Consider the following example:
```
function Car(make, model, year) {
	this.make = make;
	this.model = modell;
	this.year = year;
}

var myCar = new Car("Honda", "Civic", 2009);
console.log(myCar.year); // 2009
```
When we call `Car()` with a new constructor in front we have followed the steps we outlined above which sets the ```this``` value for the call of `Car()`. Essentially, this is the most powerful way to determine the value of ```this``` and will overwrite any other uses of call(), apply(), or bind(). 

Learn more about the nuances of determining the context of the keyword this [here](https://github.com/getify/You-Dont-Know-JS/blob/master/this %26 object prototypes/ch2.md#everything-in-order).
### Can We Go Home Now?
Well, what is there left to say? You might not like to hear it, but we have barely brushed the surface of the implications of binding the keyword ```this``` in JavaScript. Let’s summarize what we have gone over here before we close out. 

First we saw how the keyword ```this``` is analogous to the use of pronouns in the English language. We use it in place to hold the value of something (proper nouns in English or objects in JS land) to access at another time in our program. 

We then learned the fundamental concept of the keyword ```this```: it is assigned the value of the object that invoked the function in which it is called.

Finally, we looked over three important concepts for setting the value of the keyword ```this``` at the call-site either through explicit binding, implicit binding, new binding, or default binding to the global variable.

I hope this post can help you understand this concept with more clarity and can help you to use the keyword ```this``` with confidence. Just like with everything in this world, there are exceptions to the rules that were outlined above; however, they are out of the scope of this blog post and I am sure someone, somewhere, has already written about them. As always, Google is your best friend.

Onwards!
