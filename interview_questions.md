#Practice Interview Questions With Student Answers

The master list of questions that we've asked students in mock interviews and group interview practice sessions. **If you are a student and want to contribute answers, please make a pull request**

##Character Questions

Do you think anyone can learn to code?

What is the most important thing you learned at gSchool?

Do you have any pet projects?

What is your dream job?

What books are on your reading list?

If you could master one technology this year, what would it be?

Do you prefer to work on a team or alone?

Who are your favorite developers/bloggers that you follow?

Who are your heroes?

What open source-contributions have you made?

What did you learn this week?

***

##Short-Answer Technical Questions

What’s the difference between Bignum and Fixnum?

How do symbols differ from strings?
>Symbols are immutable.

What is convention over configuration?  
>Convention has a set way of doing things, and the framework requires you to program a particular way. The benefits are that unimportant choices are abstracted away. The downside is that you have to conform to the correct way of doing things.

What's the function of garbage collection in ruby?
>To clear up places in memory that no longer have any pointers connected to them. Free up space.

What are the 3 worst defects of your favorite programming language?

What's the difference between render and redirect in Rails?

>Render renders a particular view using the instance variables available in the controller action. Rails creates the html for that view and returns it to the browser. Redirect sends a redirect to the browser, telling it to re-request a new URL. The browser will send a new request to the URL and go through the action for that URL, and none of the variables created in the action that caused the redirect will be available to the redirected view.

Describe the Rails Asset Pipeline and how it handles assets(such as JS and CSS files)

>The asset pipeline provides a way to concatenate and minify/compress JS and CSS assets.

>Render communicates to rails what view to utilize while crafting the response(it does this without passing any data to the next controller action), while redirect simply tells the browser to make a new request to a different URL(this will pass data).

>The asset pipeline's purpose is to compress the JS and CSS assets. It does this by precompiling, concatenating and minifying those assets into one single path. Essentially it takes all of your javascript files, images, and stylesheets before then joining them into the public/assets folder.

What is an ORM?
>Object Relationship Mapping, it connects data in your database with functionality in your models to create objects.

>An ORM (for object relational mapping) is a tool that lets you access and change data from a database using an object paradigm. Instead of writing raw SQL and talking to the database directly yourself, you use an ORM to produce the code needed to interact with the database. ActiveRecord serves this purpose for Rails.

What is the database.yml file?

>The database.yml file in Rails is a configuration file that contains information about connecting to the appropriate database for the current Rails environment. It uses YAML, a data serialization standard. It configures this information for development, test and production environments (Rails expects a different database for each environment). Typically you do not commit this file to github.

What are the 3 data sources that the params hash is compiled from?

>path variables,request body, and query string.

What are the different rails environments?  Why do they exist?  What are the differences between them?

>The three different rails environments are production,development,and test. These three configure the rails framework. Development turns off caching, making development faster. Production allows caching, and Test has a special database of its own that is then thrown away after each test runs.


Write code to produce a `stack level too deep` error

```
def this_method
  this_method
end
```
What are data-attributes and why are they useful?
>They let you place information on a dom object so that you can easily recall it later in your code, or with some other dom interaction.

>Data attributes are part of HTML5. They let you store snippets of data in the DOM, for example if you want to store an ID with something but don't want it to appear visible on the page. Before HTML5, you had to store data in class or rel attributes, which sometimes caused problems.

In as much detail as possible, explain what happens when I type 'google.com' into my navbar and hit enter.

What is a typical use case for anonymous functions?

>Callbacks, like in the .then of an AJAX call.

Name 2 ways to define a global variable in Javascript
>Leave off the `var` or assign it to the `window`

What does AJAX stand for?  Explain how it works in as much detail as possible
>Asynchronous json and xml, it just makes a request to a specific url with a verb and data (and callbacks). Then it makes the call with the appropriate headers.

What’s the difference between `==` and `===` in JS?

>Type Coercion


> == doesn't care about type (i.e. type coercion), so "2" == 2 will evaluate to true. === does care about type, so "2" === 2 will evaluate to false.

In Ruby, what’s the value of x: `x = 10 + '20' `

>This will throw an error, because you're trying to add a string to a number.

In Javascript, what’s the value of x: `var x = 10 + '20' `
>'1020'

What does the following JS code return:

```
var a = [1,2,3]
var b = [1,2,3]
return a === b

```
>false

What's the difference between Primitive and Reference types in Javascript?

>A primitive type has a fixed amount of memory that it takes up, where as a reference type does not. Examples of primitive types are boolean values or integers, where as examples of ref types would be arrays. ref types like arrays are made up of references to their values, hence the name

---
The code will return "false", this is because the variables a and b represent different locations in memory. However the following code would return true in the way we would expect as variable b is set to represent a, and has the same location in memory.

```
var a = 1
var b = 1
a === b

```

What is the result of running following JS code:

```
var foo = "Hello";
(function() {
  var bar = " World";
  alert(foo + bar);
})();
alert(foo + bar);
```

Explain this ruby idiom: `a ||= b`

>It behaves like 'a = a || b'. If the left side evaluates to true, the right side is not evaluated. If the left side evaluates to false or nil, a is set to equal b.

>this is considered somewhat shorthand for
"a || a = b"

>what it says is if a is false, then evaulate b and set the variable a to the value of b.


Order the following CSS selectors by specificity

```
p
#special
.selected
div p
.red .green .blah

```

What does CSS Stand for and what does its name mean?
>Cascading Style Sheets. Refers to the inheritance of style rules from parent elements.

How is CSS Specificity calculated?
>A running point total is tallied by from CSS selectors for a given rule. Different selectors are worth different amounts of points. Inline styles are 1000, IDs are 100, classes/attributes are 10, elements and pseudoselectors are 1

Give me an example of a function that cannot be rewritten recursively

What is z-index in CSS?
>It's the z axis in a 3 dimensional system. Objects with a greater z index will appear to sit above of those with a lower z index.

Name 3 color systems in CSS
>RGBa, HSLa, HEX, HTML5

>RGBA, Hexadecimal, Keyword


Name 4 different media queries in CSS
>Device height, device aspect ratio, device width, orientation
How do you go about testing your JavaScript?

What is a relational database and how does it differ from a non-relational database?  Give examples

>Relational databases are composed of various tables that are 'related' by associations made from among the table entries. Non-relational databases have no table schema, instead they have individual models within whichall associated data is contained. Any SQL database is relational, MongoDB is an example of a non-relational DB.

>A relational database is based on the relational model. It organizes data into tables of columns and rows. Each one of these rows will have its own key. It's because of these keys that we can link a row to another by using its key, or as its called "a foreign key". Relational databases use SQL to query and change the database

>Examples: PostgreSQL, MySQL.

>A non-relational db does not use the same table/key model as a relational one. These types of databases are made to scale and handle much large amounts of data. Rather than use tables/keys, they use their own special frameworks.

Examples: NoSQL, MongoDB
---

WTF is REST?
>REST is an architecture for building consistent web applications. A fundamental concept of REST is CRUD. The basic functionality should allow for Creating, Reading, Updating, and Deleting.

>REST is an architecture style for designing web applications that utilizes HTTP to communicate between machines. These types of applications use HTTP requests to do CRUD operations. REST is considered a lightweight alternative to other architecture styles.


What does `git bisect` do?

>Git Bisect employs binary search to discover when a bug (surfaced by a subcommand) was introduced.

>git bisect will utilize binary to search different states of your code with the goal of finding the change that created/introduced a bug.


How would you design a URL shortener similar to bit.ly?


***


##Whiteboard Questions

Write a method to check if 2 given words are anagrams.

```
anagram_checker("Dictionary", "Indicatory")
#=> true

anagram_checker("Dictionary", "blahblah")
#=> false

```

Write code to convert a numeric string like “543” and convert it to the integer version 543. Assume numbers will be whole integers.

What is 595 in binary?
>1001010011

Convert 101101 to base 10
>45

Whiteboard the schema for zappos.com

Write FizzBuzz with as few if statements as possible. It's possible without any conditionals at all.

Implement a function which calculates the n-th item of Fibonacci sequence

Find largest prime palindrome less than 1000

Implement an algorithm to reverse a singly linked list

Count the number of nodes in a binary tree

Write your own getElementById function
