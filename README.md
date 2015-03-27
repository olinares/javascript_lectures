# javascript_this

##  An Introduction of `this` with JavaScript
Today, we're exploring one of the hardest concepts to learn in JavaScript: the reserve word `this`. Based on my experience, many developers struggle to learn this concept due to an oversimplification of how it's often taught. In many situations, authors, bloggers, and developers attempt to reveal the mystery of `this` with an all-encompassing statement: "Always look to the left of the dot operator."

For a period of time, this advice adequately informed my understanding of `this`. With more time, I've found moments where I've read or written code where this advice felt inadequate. There were several moments, for instance, where "looking at the left of the dot operator" generated more confusion than englightenment. 

To decrease your liklihood of having similiar confusion, we'll discuss three scenarios where "looking at the left of the dot operator" often doesn't work. 
 

### Objectives 
During this workshop, we'll have three objectives: 

students will be to...

1. understand `this` with code flow
2. understand `this` with expressions
3. understand `this` with callbacks

#### 1 of 3: Code Flow!
In this section, I'm going to declare a variable named `minionOne` and initialize it to an object literal. Within this object literal, we are going to create a property (`name`) and a method (`introducteYourself()`). In the definition of our method, we include the reserve word `this`. 

```javascript
var minionOne = {
  name: "Kevin",
  introduceYourself: function() {
    return "Hello, my name is " + this.name + ".";
  }
};

// "Hello, my name is Kevin."
minionOne.introduceYourself();
```

When we invoked `minionOne.introduceYourself()`, we'll notice in the output that `this.name` was resolved to "Kevin."" We can form the loose connection that "looking to the left of the dot operator" translates into looking to the left of `minionOne.introduceYourself()`. I find this to be a huge leap of faith. 

Instead of faith, let's use code flow. When we invoke `minionOne.introduceYourself()`, we begin the following process: 

1. We search for the object that `minionOne` references, which we find.
2. We search for a method named `introduceYourself()`, which we find.
3. We execute the `return` statement. 
4. We notice `this.name`, which requires us to determine the value of `this`.

At this moment, we can determine the value of `this` with a question I've developed: "Who(m) made me do this?" In other words, what's the name of the current method--`introduceYourself()`. Then ask yourself, "Who(m) made me introduce myself?" 

The answer is found on the line of code that invoked this method: `minionOne.introduceYourself()`. We now know that `minionOne` made me introduce myself. Let's apply this new information and substitute all instances of `this` in `introduceYourself` with `minionOne`. 

```javascript
var minionOne = {
  name: "Kevin",
  introduceYourself: function() {

    // original
    // return "Hello, my name is " + this.name + ".";

    // substituted 
    return "Hello, my name is " + minionOne.name + "."; 
  }
};
```

Reading the updated version of our code, we can clearly see that `minionOne.name` resolves to `"Kevin"`. 

***
#### Exercise 1 of 3: 
Explain the flow of the following code: 

```javascript
function Minion(name) {
  this.name = name;
};

Minion.prototype.introduceYourself = function() {
  return "Hello, my name is " + this.name + ".";
};

var minion = new Minion("Cho");

// What's the output?
minion.introduceYourself();
```
***

#### 2 of 3: Expressions!
In this section, we'll explore another situation where "looking to the left of the dot operator" will generate more confusion than enligthenment. 

We will use the following code to create our scenario:

```javascript
var minionOne = {
  name: "Kevin",
  introduceYourself: function() {
    return "Hello, my name is " + this.name + ".";
  }
};

var minionTwo = {
  name: "Dave",
  introduceYourself: minionOne.introduceYourself
};

// Hello, my name is Dave.
minionTwo.introduceYourself();
```

In the above code, we've declared a variable named `minionTwo` and initialized it to an object literal. We also defined a property (`name`) and a method (`introduceYourself()`). Unlike `minionOne`, we didn't re-implement `introduceYourself()`. Rather, we re-used it from `minionOne`! 

In this situation, we can "look at the left of the dot operator," but which dot operator--`miniontwo.introduceYourself` or `minionOne.introduceYourself`? We can resolve this problem with an understanding of expressions. Let's repeat the code flow we used during the first section of this workshop: 

1. We search for the object that `minionTwo` references, which we find.
2. We search for a method named `introduceYourself()`, which we find.
3. We notice that the value of `introduceYourself()` is `minionOne.introduceYoursef()`, which is an object and a method. 

Based on a cursory read of this method, the value of `minionTwo.introduceYourself` is `minionOne.introduceYourself`. With further inspection, we realize that this is partially correct. The value of `minionTwo.introduceYourself` is the resolved value of `minionOne.introduceYoursef()`, which is a function.

If this logic seems confusing, view the following example: 

```javascript
var villian = {name: "Gru"};

var name = villian.name;

// "Gru"
name;
``` 

In this example, you'll notice that `name` returned `"Gru"`, not `villian.name`. 

Let's apply this new knowledge to our minions example: 

```javascript
var minionOne = {
  name: "Kevin",
  introduceYourself: function() {
    return "Hello, my name is " + this.name + ".";
  }
};

var minionTwo = {
  name: "Dave",

  // original 
  // introduceYourself: minionOne.introduceYourself

  // substituted 
  introduceYourself: function() {
    return "Hello, my name is " + this.name + ".";
  }
};

// Hello, my name is Dave.
minionTwo.introduceYourself();
```

***
#### Exercise 2 of 3: 
Explain the flow of the following code: 

```javascript
function Minion(name) {
  this.name = name;
};

Minion.prototype.introduceYourself = function() {
  return "Hello, my name is " + this.name + ".";
};

var gollum = {
  name: "Gollum",
  introduceYoSelf: Minion.prototype.introduceYourself 
};

// What's the output? 
gollum.introduceYoSelf();
```
***

#### 3 of 3: Callbacks
In this section, we'll explore the use of `this` with a callback.

Here's our scenario: We'll create a function named `introduceYourself`, and it will have two parameters: `obj` and `callback`. When invoked, `introduceYourself` will enable any object to introduce itself with any introduction we pass as the callback.  

```javascript
var minionOne = {
  name: "Kevin",
  introduceYourself: function() {
    return "Hello, my name is " + this.name + "."; 
  }
};

function introduceYourself(obj, callback) {
  return callback.call(obj);
}; 

// "Hello, my name is Bart Simpson."
introduceYourself({name: "Bart Simpson"}, minionOne.introduceYourself);
```

When we look at the above code, the most unfamiliar line should be this: 

```javascript
  return callback.call(obj);
```

This one line of code appears to be deceptively simple. This isn't the case. A lot is happening, and I'll discuss what's happening with the following code flow: 

1. We take our callback (`minionOne.introduceYourself`) and invoke a method (`call`) on it. 
2. The method (`call`) accepts one argument (`obj`).
3. Behind the scenes, `this` points to `obj`. 

In other words, this is a process for changing the value of `this`. 

***
#### Exercise 3: 
Binding the value of `this` to a context is a common task in JavaScript. This is so common that you'll see developers creating or using the following code (below). Review this code and try to explain what it's doing: 

```javascript
Function.prototype.bind = function(context) {
  var func = this;
 
  return func.apply(context);
};

var introduceYoself = function() {
  return "Hello, my name is " + this.name + ".";
};

var cho = {
  name: "Cho"
};

var colt = {
  name: "Colt"
};

// what's my output?
introduceYoself.call(cho);

// what's my output?
introduceYoself.call(colt);

// Bonus: what's my output? Why?
introduceYoself.apply(cho);
```
***

## Conclusion
The reserve word `this` is a hard concept to learn. Much of the confusion associated with it stems from an oversimplification in how it's taught. I hope the scenarios that we covered today has improved your understanding of it. 
