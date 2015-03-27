##  An Introduction to Inheritance with JavaScript
When learning how to code and, especially, learning about  object-oriented programming, you will inevitably learn about the concept of inheritance.

As you will learn, inheritance affords us visible and invisible benefits. The visible benefits inform the way we write code. The invisible benefits explain why writing code this way is immensely valuable.  

Many junior-level developers cannot explain with confidence the visible or invisible benefits of inheritance. You will not become one of these developers! In this lecture, I'll introduce you first to the invisible benefits; and then the visible benefits. Let's start!

### Objectives 
To provide you with tangible goals for this lecture, I've defined the following six objectives:

students will be to...

(Part 1: Comprehension)
<ol start="1">
  <li>provide a non-code-related example of inheritance</li>
  <li>provide a code-related example of inheritance</li>
  <li>describe three benefits of inheritance</li>
</ol>

(Part 2: Implementation)
<ol start="4">
  <li>implement inheritance with an object literal</li>
  <li>implement inheritance with the create method of Object</li>
  <li>implement inheritance with a constructor</li>
</ol>

## Part 1: Comprehension
#### 1 of 6: A Non-Code-Related Example with Customer-Support

A customer-support-system is an excellent example of inheritance and its benefits. Let's imagine that we are creating a new system and hiring three customer-support specialists. Each specialist is given an employee identification number, an employee email address, and an employee troubleshooting library that is a gigabyte in size.

When a customer contacts one of our specialists, they will normally ask a question. When the question is asked, the specialists look for an answer in our library; ideally, the specialist finds the question and then an answer our library.  After the answer is found, our specialist provides the answer to the customer.

Everything works as designed. Now imagine that we add 10 more employees; furthermore, each employee is given the same three things as our first three specialist--identification number, email address, and library. If we pause for a moment and analyze this process, we will make the following observation: a specialist's identification number and email address must be unique; however, the troubleshooting library is identical for each specialist.

In other words, we are using 13 gigabytes to store 1 gigabyte of unique data. This is an inefficient design due to the amount of duplication. Whenever we hire a new employee, we are duplicating the library. Whenever we modify the library, we have to also update each copy of the library!

In this context, we and our specialist would be served better if they all could reference the same library. Using this design, we use one gigabyte of space to store the library. Moreover, we can update this library once. Since each specialist is referencing the same library, all specialists will have immediate access to the updates. What we are describing is inheritance!

#### 2 of 6: A Code-Related Example with JavaScript Objects
Similar to inheritance with a customer-support system, JavaScript uses the concept of inheritance to re-use code that would be identical between objects. All of you have witnessed JavaScript's use of inheritance, many of you may be just unaware of it.

The following examples will illustrate this point.

```javascript
var obj = {};

// ...TypeError: undefined is not a function
obj.speak();
```

Invoking `speak()` outputs an error, which states that the method is `undefined`. If we want to invoke a method named `speak()`, we need to define it:

```javascript
var obj = {};

obj.speak = function() {
  return "I can speak!"
};

// "I can speak!"
obj.speak();
```

Now, let's try to access a method named `constructor()`, which we have not defined:

```javascript
var obj = {};

obj.speak = function() {
  return "I can speak!"
};

// "I can speak!"
obj.speak();

// Object {}
obj.constructor()
```

Notice that invoking `constructor` did not output an error! In other words, it is defined somewhere else and being inherited here!. All objects are designed to inherit specific methods.

(Specifically, all objects inherit methods from `Object.prototype`, which we will explore later in the lecture.)


#### 3 of 6: Three Benefits of Inheritance
At this moment, we've discussed the uses of inheritance with non-code related and code related examples. Both examples are trying to convey the benefits of using inheritance. If these benefits are unclear, remember the following three benefits of inheritance:

- Re-use of Code
- Consistency of Code
- Real-Time Updating of Code

***
#### Exercise 1:
Find a pair and explain to your pair your understanding of inheritance. In your explanation, try to mention a real-world example that conveys the benefits of inheritance.
***

## Part 2: Implementation
Every object in JavaScript inherits methods and properties from something known as a prototype, which is an object. In order to implement inheritance with JavaScript, we need to use prototypes. Equally important, the way we interact with an object's prototype changes based on the way we create an instance of an object.

If this seems confusing, don't worry. We will demonstrate what this means with the following three sections.

#### 4 of 6: Implementing with an Object Literal (`{}`)
Let's create two instances of an object with object literals. Each of these objects represent instances of a minion.

```javascript
var minionOne = {};
var minionTwo = {};
```

Minions are able to talk; minions love bananas. Lets create a function named `sayBanana()` that allows both minions to say "banana.""

```javascript
minionOne = {
	sayBanana: function() {
	  return "banana";
	}
};

minionTwo = {
	sayBanana: function() {
	  return "banana";
	}
};

// "banana"
minionOne.sayBanana();

// "banana"
minionTwo.sayBanana();
```

Since the implementation of `sayBanana()` is identical for both minions, this is a moment where we would want our minions to inherit this method. (This is analogus to each of our customer-service reps receiving the same library; moreover, we want to remove the duplication of the same library.)

An object literal, however, is very restrictive in the way it allows us to modify its prototype.  Whenever an object literal is created, it will automatically inherit from `Object.prototype`--an object--and this default behavior cannot be changed.

In this context, the only way to have both minions inherit `sayBanana()` is adding this method to `Object.prototype`. Doing this will cause untended consequences.

```javascript
Object.prototype.sayBanana = function() {
	  return "banana";
};

// "banana"
minionOne.sayBanana();

// "banana"
minionTwo.sayBanana();

var gollum = {};

// "banana"
gollum.sayBanana();
```

 Since all objects inherit from Object.prototype, all objects will now have a method named `sayBanana()`. Even gollum can say "banana!"

#### 5 of 6: Implementing with Object's Create Method (`Object.create()`)
If we do not want all objects to inherit `sayBanana()`, we must create our instances of a minion with a different syntax: `Object.create()`. This method of Object accepts an argument that changes the prototype chain of an object. This will make more sense with a few examples.

```javascript
var prototypeObject = {
  sayBanana: function() {
    return "banana";
  }
};

var minionOne = Object.create(prototypeObject);
var minionTwo = Object.create(prototypeObject);
```

The above code creates two instances of an object that represents a minion. Both minions prototype also point to `prototypObject`, which contains `sayBanana()`. The benefit of this approach is not having all objects inherit `sayBanana()`--just the objects that are passed `prototypeOjbect`.  

Here's a very subtle but important thing to remember: Since `prototypeObject` is an object literal, it inherits from `Object.prototype`. In other words, both minions inherit from `prototypeObject` and `Object.prototype`!

```javascript
var prototypeObject = {
  sayBanana: function() {
    return "banana";
  }
};

var minionOne = Object.create(prototypeObject);
var minionTwo = Object.create(prototypeObject);

// "banana"
minionOne.sayBanana();

// "banana"
minionTwo.sayBanana();

var gollum = {};

// ...TypeError: undefined is not a function
gollum.sayBanana();

// Object {}
minionOne.constructor();

// Object {}
minionTwo.constructor();

// Object {}
gollum.constructor();
```

#### 6 of 6: Implementing with a Constructor ([[Constructor]].prototype)
Using `Object.create()` works as we intend, but it's reptitive. If we want to create hundreds of new minions, we need to create hundreds of new objects and make them resemble a minion. The better approach to creating an instance of a minion is using a constructor named `Minion`.

```JavaScript
function Minion() {
}

var minionOne = new Minion();
var minionTwo = new Minion();
```

Perfect, we are now creating objects with a constructor. Since this is another way of creating an object, we must use a different approach for modifying the prototype of these objects.

When dealing with constructors, we interact with the prototype of all instances of a constructor via a constructor's property named `prototype`:

```javascript
function Minion() {
}

Minion.prototype.sayBanana = function() {
  return "banana";
};

var minionOne = new Minion();
var minionTwo = new Minion();

// "banana"
minionOne.sayBanana();

// "banana"
minionTwo.sayBanana();
```

All minions now inherit `sayBanana()`; moreover, our code is semantically meaningful. We aren't creating just objects; we are creating minions.

***
#### Exercise 2:
Create an instance of something--e.g. penguin from Madagascar--and have it inherit a method. Create your thing using each of the three ways we've described and their corresponding approach for modifying a prototype.
***

## Conclusion
In object-oriented programming, inheritance provides a mechanism for writing maintainable code. If you understand this, you will not only learn a new way of writing code, but you will also find yourself understanding the immense value of writing code this way--re-use of code, consistency of code, and real-time updating of code.

I hope that this lecture has taught you how to both comprehend the concept of inheritance and how to implement the concept of inheritance with JavaScript.
