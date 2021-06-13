# Notes

[TOC]

# General

* Mozilla Developer Network

# Sublime Shortcuts

* html + tab for boilerplate code
* Any tag + tab

# HTML

* thead
* tbody
* &lt;label> tags used for visually impaired
  * Label tag’s “for” and input tag’s “id” must match
* “name”=”value”
  * “name” attribute is sent as parameter key
    * It is also used to group radiobuttons or checkboxes together
  * “value” attribute is sent as parameter value
* Input validation
  * “pattern”={5,10} paired with “title” is better than “minlength” and “maxlength”

# CSS

* strong / em vs. bold / itatlic
* descendant tags - “li a” means “all a tags within li tags”
* Adjacent tags - “h4 + ul” means “all ul tags after h4 tags”
* Attribute tags - “a[href = “[www.google.com](www.google.com)”] means “all a tags with href=[www.google.com](www.google.com)”
* Nth type tags = “li:nth-of-type(3)” means “every 3rd li tag”
* Specificity - #id > .class, attribute > element, adjacent, descent
* Pixel size: em is relative to the text it is in. e.g. 5.0em is 5x bigger than the paragraph it is with.
* font-weight ranges from 100-800

# Bootstrap

* Forms
  * form-control makes the components look like bootstrap
  * form-group lumps the correct components together so that they look related
* Nav
  * navbar-collapse is what will hide the navbar options when it’s shrunk to mobile view
  * data-target specifies the id of which options to apply the hamburger to
* Bootstrap 4
  * Responsive breakpoints and margins
  * There is no xs, so just dont specify
  * Anything that is specified is applied upwards until it’s overridden
    * d-s-block will display the div as a block from small to xlarge
    * The alternative is d-s-none which hides it.
  * Hiding and showing blocks is useful when we want to hide certain paragraphs when on mobile, and only start to show it when expanded
  * container-fluid is full screen whereas container has padding

# Flexbox

* Note that flexbox is not a Bootstrap specific component
* First set the div with `class=d-flex`, by default it is `flex-row,`which make the main axis the x-axis, but you can set main axis to column by using `flex-column`
  * justify-content aligns main axis
  * align-item aligns secondary axis
* Grid specifies how wide they are, flex specifies where they should be

# Javascript

    *   Variables
        *   null vs. undefined
            *   null is explicitly nothing, while undefined just means it’s nothing yet
    *   Conditions
        *   == checks only for value 5 == “5” is true
        *   === checks for both value and type 5 === 5 is false
    *   Functions
        *   It’s ok to not send function parameters, it will just be undefined
        *   Declarations vs. Expression - when done as an expression, it can be overwritten
        *   `var funcVar = function testFunction( ) { };`
        *   Higher Order functions - sending function within function
            *   `function sing( ) {...} \
setInterval(sing, 1000) // calls sing every 1000ms`
            *The reason sing does not have ( ) is because we do not want it to execute immediately, e.g. in the below, the italic parts only declare the function without a name. It’s the bolded () that actually invokes it. \
<code><em>(function() { \
    console.log("This is an anonymous function"); \
})<strong>()</strong></em>;</code>
            *   Anonymous functions declares function inline, dont have to give it a name.

            ```
            setInterval(function( ) {
    console.log("This is an anonymous function");
}, 2000); // where 2000 is 2 milliseconds
            ```

        *   Arrays
            *   push()/pop() adds/remove to the end.
            *   unshift()/shift() adds/remove from the front.
            *   indexOf() checks if something exists in array, returns -1 if not.
            *   slice() makes a copy of it, takes 2 arguments for start and end.
            *   foreach syntax - `array.forEach(anotherFunc)` \
`colors.forEach(function(color) { \
    console.log(color); \
} // color is each element in the array`
            *   Specifying own version of foreach to be made available to arrays in general. So that we can call arr.myForEach(function() {});`\
Array.prototype.myForEach = function(func) { \
  for(var i=0; i&lt;this.length; i++) { \
    func(this[i]); \
  } \
}`
            *   `WordsArray.reduce((result, word) => result.replace(word, ""), str).trim();`
            *The reduce function is used to loop through an array and apply it to a cumulative result.
            *   The above example looks through `WordsArray` in `str` and replaces it with “”, then return `result`
    *Regex
        *   Javascript is in format /.../
            *E.g. `/[^a-z0-9]/gi`
            *   `g`represents``global - so it wont stop just at first one
            *   `i`means case insensitive

## ES6 / ES2015 Syntax

* Template strings using Backticks ``
  * <code>console.log(<strong>`${parsedData.name} lives in ${parsedData.address.city}`</strong>);</code>
    * <code>`` - </code>must use backticks
    * Everything within <code>${}</code> will then be interpreted as variables
* Arrow Functions
  * Removed the word function, just retain parameters and add <strong><code>=></code></strong>
  * <code>var add = (a,b) => { \
    return a+b; \
}  \
// can be further refactored into \
var add = (a,b) => a+b; // no more return keyword</code>
  * <code>[1,2,3].map(value => value *2);</code>
  * Single param functions dont need parenthesis
    * <code>var doubleAndFilter = <strong>arr</strong> => arr.map(<strong>value</strong> => value*2).filter(<strong>value</strong> => value%3 === 0);</code>
  * Arrow functions vs normal functions
    * AF do not get their own keyword <code>this</code> and<code> arguments</code>
    * <code>this</code> refers to what it will be immediately outside of the arrow function
      * Useful in async function
[example](#heading=h.kqjeqy441ei) so that we no longer use bind and can be refactored to
      * <code>sayHi: function() { \
    setTimeout(() => console.log("hello " + this.firstName)); \
};</code>
      * It is not used for the <code>sayHi</code> method because it will no longer have its own keyword <code>this</code>, and will refer to the global object (e.g. <code>window</code>)
    * <code>arguments</code> will work in inner function to obtain arguments of outer function - solved by using keyword <code>rest</code>
  * When NOT to use
    * For methods in objects - because no keyword <code>this</code>
* [Promises](#heading=h.78rym4f88jeo)
  * For express to handle requests
    * <code>npm install request-promises; // note that request is a dependency</code>
    * <code>const rp = require("request-promise"); \
<strong>rp("[http://www.google.com](http://www.google.com)") \
.then( function(htmlString) {...}) \
.catch( function(err) {...});</strong></code>
* <code>let...await</code>
  * <strong><code>let campground = await Campground.create(seed);</code></strong>
  * Wait for <code>create()</code> to finish, then assign the value to campground
* <code>for(const dog of dogs) replaces foreach</code>
* <code>const</code>
  * Primitive types are immutable. But objects like arrays (e.g. push and pop) can be changed, just not declared
* <code>let</code>
  * Block scope
  * Note that <code>let</code> inside of function is not the same as <code>var </code>because of hoisting
* Default parameters
  * <code>function add(a=2, b=4) {...}; // a will be defaulted to 2 if it's not sent</code>
* <code>for...of</code>
  * <code>For...<strong>in </strong></code>is traditionally used to loop through keys of objects
  * <code>For...of</code> is used to loop through values with a Symbol.iterator (e.g. Arrays, Strings, Maps, Sets)
* <code>Rest operator ...</code>
  * Basically used to denote all remaining arguments, and will be put into an array
  * <code>function add(a,b,<strong>...c</strong>) {...}; \
add(1,2,3,4,5); // returns 1,2, [3,4,5];</code>
* <code>Spread operator ...</code>
  * Makes array into csv
  * E.g.1 - concat 3 arrays
    * <code>var arr1 = [1,2,3]; \
var arr2 = [3,4,5]; \
var arr3 = [6,7,8]; \
var combined = arr1.concat(arr2).concat(arr3); \
var combined = <strong>[...arr1, ...arr2, ...arr3];</strong></code>
  * E.g. 2
    * <code>var arr = [1,2,3,4,5]; \
Math.max.apply(this, arr); // Math.max takes in a series of arguments, not an array \
<strong>Math.max(...arr);</strong></code>
* Object Enhancements
  * Object Shorthand Notation
    * <code>var instructor = { \
    firstName: firstName, \
    lastName: lastName \
} \
// shortened to \
<strong>var instructor = { firstName, lastName };</strong></code>
    * <code>sayHello: function() { \
    Return "Hello!; \
} \
// shortened to \
<strong>sayHello()</strong> { \
    Return "hello"; \
}</code>
  * <code>Computed Property Names</code>
    * <code>var firstName = "Elie"; \
var instructor = { \
    <strong>[firstName]</strong>: "That's me!" \
} \
// not possible in ES5, have to separately declare \
instructor.Elie = "That's me!";</code>
* Destructuring
  * Object
    * <code>var instructor = { \
    firstName: "Elie", \
    lastName: "Chong" \
}; \
<strong>var {firstName, lastName} = instructor; // must be same name as object \
var {firstName: first, lastName: last} = instructor; // first=Elie, last=Chong</strong> \
firstName; //Elie \
lastName; //Chong</code>
    * Common to send in destructured objects as parameters to functions
      * <code>function displayInfo({name, favColor}) { return [name, favColor]; } \
var instructor = { name: "Elie", favColor: "Purple" }; \
displayInfo(instructor);</code>
  * Array
    * <code>var [a,b,c] = [1,2,3]; \
// return based on the position of the items in the array</code>
    * Helpful to swap values
      * <code>[b, a] = [1,2];</code>
* Maps (hashmaps)
  * Same as objects, but their keys can be ANY data type
  * Why use maps
    * Has a <code>size</code> property
    * Keys can be any type
    * May accidentally overwrite keys on Object.prototype - maps don’t have that issue
    * Easy to iterate with for...of
  * When to use
    * Look up keys dynamically
    * Need keys that are not strings
    * Frequently adding and removing key/value pairs
  * Methods
    * <code>.get(), .set(), .delete(),. size</code>
  * <code>WeakMap</code>
    * Better performance
    * Similar to Map, except all keys MUST be objects
    * Cannot iterate since values in it can be cleared if there is no reference
* Sets
  * All values are unique, any type of value can exist
  * Can iterate with for...of
  * When to use
    * When order is not required, and we don’t want duplicates
  * Methods
    * <code>.add(), .has(), .delete(), .size</code>
  * WeakSet
    * Better performance
    * Similar to Map, except all keys MUST be objects
* Generators
  * Generator functions allow us to pause execution, and resume later
  * How it works
    * Created using a *at the end of the function keyword (i.e. <code>function*</code>)
    * When invoked, a generator object is returned with keys <code>value</code> and <code>done</code>
    * <code>value</code> is returned from the pause function with <code>yield</code>, <code>done</code> returns <code>true</code> when function has completed
    * Call <code>.next()</code> to resume running the function
    * Can be iterated with for...of
  * Use Case
    * Time consuming functions
    * Pausing asynchronous code then continuing later
* <code>Object.assign</code>
  * Used to create copies of object
  * Start with empty object, otherwise it will still keep a reference
  * <code>var o = {name: "zixin"}; \
<strong>var o2 = Object.assign({}, o);</strong></code>
  * Does not use a deep clone - i.e. internal objects of o will still be passed by reference
* <code>Array.from</code>
  * Convert other data types into arrays - i.e. strings or array-like objects
* <code>Array.find / findIndex</code>
  * Invoked on array
  * Accepts callback(value, index, array) and returns the value/index found or undefined
  * <code>var instructors  = [{name:"zixin"}, {name:"jack"}]; \
<strong>instructors.find(val => val.name === "zixin"); // {name:"zixin"}; \
instructors.findIndex(val => val.name === "zixin"); // 0</strong></code>
* <code>String.includes</code>
  * Find if string contains another string
* <code>Number.isFinite</code>
  * Checks that a number has typeof number, and !isNaN

## ES2016 / ES2017

* ES2016
  * Exponential operator `**`
    * Replaces Math.pow
    * 2 to the power 4 - `2**4`
    * `total **= 4;`
  * `[].includes -`find if value exists in array
* ES2017
  * padStart / padEnd
    * Make string a certain number of characters by adding spaces in front/behind
    * `padStart(totalLength, charToPad="")`
  * Async functions
    * Created with keyword `async`
    * Returns a `Promise`, and resolves with what is returned from the function
    * Useful when used with `await`
      * `await`pauses execution of the async function until the promise is resolved, then resumes the async function’s execution and returns the resolved value
    * Removes need for Generator functions and nested promises or callback or yield etc.
    * Can also be placed as methods inside objects
    * Use `try...catch` to handle `Promise.reject`
    * HTTPRequests - what if we want to make 2 requests concurrently without waiting sequentially
      * We just await the promise after we make the requests
      * **<code>async function getMovieData() { \
    var titanicPromise = $.getJSON(...); \
    var shrekPromise = $.getJSON(...); \
    var titanicData = await titanicPromise; \
    var shrekData = await shrekPromise; \
    ...} \
}</code></strong>
    * Await with <code>Promise.all</code>
      * <strong><code>var movieList = await Promise.all([ \
    $.getJSON(...), \
    $.getJSON(...) \
]);</code></strong>
  * Object rest and spread
    * Rest
      * <code>var instructor = {first: "Elie", last: "Chong", job: "programmer", numSiblings:3}' \
var { first, last, <strong>...data</strong> } = instructor; \
// first: Elie \
// last: Chong \
// data: {job: "programmer", numSiblings:3}</code>
    * Spread
      * <code>var instructor = {first:"Elie", last:"Chong", job:"programmer"}; \
var instructor2 = <strong>{...instructor, first:"Jackie", last:"Cheung"};</strong> \
// basically creates instructor2 as a copy of instructor and replace first and last</code>
      * More modern way of creating copies of objects, same as <code>Object.assign</code> in ES2016

# Object Oriented Programming

* Javascript does not have concept of objects or classes, it is replaced using constructor functions
* `this` keyword ([also read section on this, closures](#heading=h.kqjeqy441ei))
  * Global variables
  * Parent function
  * `call(), apply(), bind()`
    * `call(thisArg, a,b,c);`
    * `apply(thisArg, [a,b,c]);`
    * `bind()` returns a function so that it can be called later
* `__proto__`
  * `new keyword returns link between object and its prototype`
  * It’s like the skeleton object
* Closures
  * Applies when an inner function uses a variable defined by an outer function.
  * `function outer() { \
  var count = 1; \
  return function() { \
    return ++count; \
  } \
}`

        ```
        outer()();
        ```

  * Useful to create private variables
* Constructor functions start with caps - not mandated by JS but good practice so that other developers know
* `new` does 4 things
  * Creates empty object
  * Sets the keyword `this` to be that empty object
  * Adds `return this` to the end of the function
  * Adds a property to the object `__proto__`,this links prototype property on the constructor function to the empty object
* Reusing a constructor in another
  * E.g.
    * <code>function Car(make, model) { \
    this.make = make; \
    this.model = model; \
    this.numWheels = 4; \
} \
 \
function Motorcycle(make, model) { \
    <strong>Car.call(this, make, model); \
    Car.apply(this, [make, model);</strong> \
    this.numWheels = 2; \
}</code>
    * By using <code>call() </code>or<code> apply()</code>, we make the this in Car refer to Motorcycle
    * Even better refactor
      * <code>function Motorcycle() { \
    Car.apply(this, <strong>arguments</strong>); \
    … \
}</code>
      * <code>arguments</code> basically return an array-like object (has length, but no for...of) of whatever was sent into the function, even if we didnt specify in the function declaration
  * Prototypes
    * Every constructor has a .prototype which links to the prototype object
    * Every prototype object has a .constructor that links to the constructor function
    * When new keyword is used, it links the object to the constructor via <code>.__proto__</code>
    * <code>var mazda = new Car(...);</code>

            ```
            mazda.__proto__ === Car.prototype;

Car.prototype.constructor === Car;
            ```

        * ![alt_text](images/image1.png "image_tooltip")

        *   Prototype Chain
            *   When Javascript looks for a method, it looks up the .__proto__ chain to find it, otherwise returning undefined.
            *   __proto__ chain can be thought of as inheritance
        *   Adding methods to prototype
            *   <code>// the below is inefficient because each new object created from Person will then have its own definition of sayHi \
function Person(name) { \
    this.name = name; \
    this.sayHi = function() { return "Hi " + this.name; } \
} \
 \
// using __proto__ is more efficient because then every object can share it \
function Person(name) { \
    this.name = name; \
} \
<strong>Person.<em><span style="text-decoration:underline;">prototype</span></em>.sayHi = function() { return "Hi " + this.name; };</strong></code>
    *Inheritance
        *   Don’t pass one constructor to the other, pass the prototype instead.
        *Don’t set one prototype to reference another, because changing one will also change another due to pass by reference
            *   <code>Student.prototype = Person.prototype; \
Student.prototype.status = 1; // this will also add a status to Person.prototype</code>
        *Solution
            *   <code>Student.prototype = Object.create(Person.prototype); // good for prototypal inheritance, other using new will add other unnecessary properties \
Student.prototype.constructor = Student; // without this step, constructor will still reference Person because of previous step</code>

* ES2015<code> class</code>
  * <strong><code>class Student { \
    constructor(firstName, lastName) {...} \
    sayHello() {...} \
    static isStudent(obj) {  \
        // static is for when don't want to create object just to use method \
        return obj.constructor === Student  \
    } \
} \
var ellie = new Student("Elie", "Chong");</code></strong>
* ES2015<code> Inheritance</code>
  * <code>class Student extends Person { … }</code>
  * Use <code>super</code> to send arguments to parent methods - methods must have <strong>SAME NAME</strong> for it to work

# DOM (Document Object Model)

* Every HTML document is translated into a series of Objects using DOM
* `console.log(document)` will give you the HTML, and `console.dir(document)` will list all the attributes inside the document
* Select elements
  * `var h1 = document.getElementById("id");`
  * `var h1 = document.getElementsByClassName("bolded");`
    * Returns as a CollectionList, it’s like an array but with some differences. e.g. length property exists but then cant do forEach
  * `var h1 = document.getElementsByTagName("h1");`
  * `var h1 = document.querySelector(".id");`
    * Can just give in a CSS style selector (e.g. #id, .classname)
    * Returns only the FIRST element when used with a class
  * `var h1 = document.querySelectorAll("h1");`
    * Returns ALL elements
  * They are all returned as Javascript OBJECTS
* Manipulate by doing `h1.style.color = "pink"`
  * `style`has everything inside CSS
  * Separation of concerns means you specify a class with everything that is supposed to be changed (e.g. change colour, font size etc.). And then use Javascript to add/remove the class on behavior change (e.g. click a button or scroll past a place)
    * `var someID = document.querySelector(".id");`
    * <code>someID.<strong>classList </strong></code>gives you the list of classes this object currently has.
    * <code>someID.classList.add/remove</code>
    * <code>someID.classList.toggle </code>switches it on if it’s currently off and vice versa
  * <code>textContent</code> retrieves all the text within the tag, including nested elements excluding the tags. E.g. this is bold text
  * <code>innerHTML </code>retrieves all the text within the tag, including nested elements AND the tags. E.g. this is &lt;strong>bold&lt;/strong> text
  * <code>getAttribute / setAttribute </code>is used to modify attributes, and is useful for changing images on sliders e.g. <code>src</code> or <code>href</code> or even <code>id</code>
* <code>element.addAddEventListener(eventType, functionToCall)</code>
  * Can have more than one listener to the same element
  * When inside the eventListener, <code>this</code> refers to the element itself - this is especially useful when dealing with bullet points or list items
  * Alternatively, determine which <code>&lt;li></code> inside the eventListener function itself

# Command Line

* `touch`creates a new file
* `rm`removes the file
* `rm -rf`removes the folder and everything in it

# Node

* HTTP body and HTTP params are not the same - form POST uses body
* `node &lt;filename>` runs the file
* `npm`
  * npm is the package manager for Node because you can’t add &lt;script> tags to your node code like in HTML
  * Installed packages go into this folder `node_modules`
  * To import the package, do `var something = require("cat-me");`
  * package.json / package-lock.json
    * Contains metadata of this package
    * `dependencies` specify which other libraries this module depends on.
    * `npm install express --save (--save) flag`when installing express will automatically include express into the current project’s package.json
  * `npm init`will help create your package.json file by asking a series of questions
  * Running test
    * npm run test to run test locally
    * npm run lint to run linting tests locally

## ExpressJS

* `express`
  * `app.get("/", function(req, res) { \
  res.send("Hi there!"); \
});`
    * .get specifies the HTTP verb. Request and response is in the function for reference, res.send prints it to the screen
  * `app.listen(PORT, function() { \
  console.log("app started on PORT"); \
}`
  * Order of Routes matter - it’s like an if..else.. statement that checks which one matches first
  * Router Parameters
    * <code>/r/<strong>:</strong>subredditName - </code>the colon makes this a parameter. Note that this is not a wild card so <code>/r/abc/def</code> will not work
    * The above can be referenced by using <code>req.params.subredditName</code>
* <code>ejs (embedded javascript)</code>
  * <code>res.render("home.ejs", {theVariable: "dog" }); </code>
    * <code>//.ejs is found in /views</code>
    * <code>The object sent in the second parameter can be referenced in the ejs file</code>
  * In home.ejs, use <code>&lt;%=theVariable%></code> to reference the variable
  * <code>&lt;% %></code> only when evaluating logic, <code>&lt;%<strong>=</strong> %></code> when displaying variable, <code>&lt;%- %></code> to evaluate and display the code (useful for rendering HTML immediately when creating blog post.
    * <code>&lt;%- %></code> is dangerous because code injection can be done. But can be prevented with sanitize package (refer to [Express](#heading=h.v9anlqujkzg) section)
  * <code>app.set("view engine", "ejs");</code> will automatically set all files to be ejs so we dont have to reference individually. Put this line at top.
* Adding CSS
  * In app.js, <code>app.use(express.static("public");</code>
    * This tells node to serve files in the <code>public</code> folder too, then put <code>app.css</code> in there
* Partials
  * Include template files to be repeated into partials, such as HTML boiler plate code
  * Partials folder is found in <code>views/partials/header.ejs</code>
  * <code>&lt;%- include("partials/header") %></code>
  * This is also where you include things like bootstrap CDN
* HTTP POST
  * <code>app.post("/createFriend", function(req, res) { \
    res.send("this is sent"); \
});</code>
  * BodyParser - a tool used to convert request.body into a JS object
    * <code>npm install body-parser // used in nearly all apps with form because POST sends into BODY</code>
    * In app.js, require it and use it
    * <code>var bodyParser = require("body-parser"); \
app.use(bodyParser.urlencoded({extended: true}));</code>
    * In app.post, reference the variable by doing <strong><code>req.body.varName</code></strong>
  * <strong><code>res.redirect("/friends"); // use this in app.post to do a redirect after POST</code></strong>
* Making API calls in Node
  * <code>npm install request</code>
  * <code>request("[http://www.google.com](http://www.google.com)", function(error, response, body){});</code>
    * Usually check<code> if(!error && response.statusCode == 200)</code>
    * body is where the actual API response content is. It is returned in a string, so you will need to use <code>var data = JSON.parse(body)</code> to parse into an object
    * Reference using <code>data["firstLevel"]["secondLevel"]["thirdLevel"][...];</code>
* Express Sanitizer
  * Used to prevent injection of code
  * <code>npm install express-sanitizer</code>

        ```
        app.use(expressSanitizer());

req.body.blog.body = req.sanitize(req.body.blog.body);
        ```

    *   Only requirement is that this must be after body-parser
    *   Generally want to sanitize where eval `&lt;%- ->` is used

* Routers
  * Cleans up all the routes in app.js by putting them into their own files
  * Create directory and file /routes/campground.js
  * Move all the routes code into each of them, require the router and models, then module.exports them
    * <code>var router = app.Router(<strong>{mergeParams: true}</strong>);</code>
    * mergeParams will share the parameters across router files. This ensures that :id can be found when we use it in app.use for commentRoutes below.
  * In app.js, require the files and app.use them
    * <code>var commentRoutes = require("./routes/comments"),</code>

            ```
            var campgroundRoutes = require("./routes/campgrounds.js"),
            var indexRoutes = require("./routes/index.js");
            ```

    * `app.use("/", indexRoutes);`

            ```
            app.use("/campgrounds", campgroundRoutes);
            app.use("/campgrounds/:id/comments", commentRoutes);
            ```

* Typical File Structure
  * `app.js - app.use("/api/todos", todoRoutes);`
  * `routes/todo.js`
    * `modules.export = router;`
    * `require(helper);`
  * `helpers/todo.js`
    * `modules.export = exports.Create, exports.Update etc.`
    * `require("../models");`
  * `models/index.js`
    * `todo = require("todos");`
    * `modules.export.Todo = todo`
  * `models/todo.js`
    * `Modules.export = todo;`

## Connect-Flash

* Used to display error messages on the next page
* Steps
  * `npm install --save connect-flash`
  * `var flash = require(...); app.use(flash());`
    * Connect BEFORE passport config
  * `req.flash("error", "Please Login First!");`
    * This will store it and allow for access in the next access.
    * Note that this does not actually display anything
  * In header file
    * <code>&lt;% <strong>if(error && error.length > 0)</strong> { %></code>

            ```
              <div class="alert alert-danger" role="alert"> <%=error%></div>
            <% } %>
            ```

* Because Error is an array, so we want to make sure there’s something in it first

## Authentication with Passport

* `npm install passport, passport-local, passport-local-mongoose`
* `passport -`package that can easily add different login strategies in
  * Tell node app that we are using passport
    * `app.use(require("express-session")({`

            ```
                secret: "Thur likes to eat bread",
                resave: false,
                saveUninitialized: false
            }));

app.use(passport.initialize());
app.use(passport.session());
            ```

* **Ordering of the commands above matters**
* Serialize and deserialize is used to encode and decode the session
        *   `passport.serializeUser(User.serializeUser());`

            ```
            passport.deserializeUser(User.deserializeUser());
            ```

  * Register new user
    * Create a new User with username, send User and password as **_separate arguments _**into `register().`
      * Only username gets shown in db in plain text, password is hashed with salt
    * `authenticate()` takes in which strategy we are using, and performs all the serialization behind the scenes
    * **<code>User.register(new User({username: username}), password, (err, user) => {</code></strong>

            ```
                    if(err) {
                        console.log(err);
                        return res.render("register");
                    } 
                    // log the user in
                    passport.authenticate("local")(req, res, () => {
                        res.redirect("/secret");
                    });
                });
            ```

* Login User
  * Tell passport to use `LocalStrategy` specified but `userSchema.plugin`
    * `passport.use(new LocalStrategy(User.authenticate()));`
  * Put `authenticate()` in `app.post,`this will run it as a middleware (code that runs between for route before callback) specifying where to go if login was successful or failure.
  * <code>app.post("/login", <strong>passport.authenticate("local", {</strong></code>

                ```
                    successRedirect: "/secret",
                    failureRedirect: "/login"
                }) ,(req, res) => {

                });
                ```

* Logout User
  * `req.logout();` // passport just destroys all your session variables
* `passport-local -`easily add username:password in
* `passport-local-mongoose -`works easily with mongoose
  * In model file, just add below after schema
    * `userSchema.plugin(passportLocalMongoose);`
* Middleware
  * standard for all middlewares to have 3 arguments, next is the next thing to be called
  * `function isLoggedIn(req, res, next) {`

        ```
            if(req.isAuthenticated()) {
                return next();
            }
            res.redirect("/login");
        }
        ```

  * Send into app.post, which will check if user is authenticated, if so, proceed with callback. Else redirect him back to login
  * Remember to add to .post command too so that people cannot postman attack
  * <code>app.post("/secret", <strong>isLoggedIn</strong>, () => {...});</code>
  * To change navbar items according to sign in status
    * Need to send user to the header file - instead of typing individually, can use the below to send to all routes (res)
    * <code>app.use(function(req, res, next) {</code>

            ```
                res.locals.currentUser = req.user;
                next();
            });
            ```

  * Refactoring middlewares
    * Create directory and file`/middleware/index.js`
    * `module.exports = { \
  checkCommentOwnership = function(...), \
  checkCampgroundOWnership = function(...) \
};`
    * In calling files,
      * `var middleware = require("../middleware/");`
      * Prepend `middleware.` to all function calls.
        * **<code>middleware.isLoggedIn</code></strong>

# MongoDB

* Common commands
  * `mongod` - starts the Mongo Daemon
    * on Mac, do `brew services start mongod-community@4.2`
  * `mongo` - starts the Mongo shell
  * `help` - instruction manual
  * `show dbs` - shows list of databases
  * `use &lt;db name>`- use the database, if doesnt exist, create it
  * <code>db.dogs.<strong>insert</strong>({name:"Rusty", breed:"Mutt"})</code>
    * <code>db</code> refers to the current selected database
    * <code>dogs</code> is the collection (or like table in MySQL)
    * <code>insert()</code> creates object in collection
  * <code>show collection </code>- show list of collections in this db
  * <code>db.dogs.<strong>find() - </strong></code>list items in db
    * <code>find() </code>- no params will list all results in collection
    * <code>db.find({name:"Rusty"}) - </code>find based on name
    * an ID gets returned when find
  * <code>db.dogs.<strong>update({objectToFind}, {objectToUpdate}) - </strong></code>takes 2 params, the search and the update
    * <code>db.dogs.<strong>update({name:"Rusty"}, {breed:"Labrador"})</strong></code>
      * This will overwrite the entire row to only have breed
    * To preserve existing items that dont need to be changed, use <code>$set:</code>
      * <code>db.dogs.update({name: "Rusty"}, {<strong>$set:</strong> {name: "Tater", isCute: true}})</code>
      * This will change the name only, retain the breed and give it a new isCute
  * <code>db.dogs.remove({objectToFind}) </code>- delete where = objectToFind
    * <code>db.dogs.remove({objectToFind}).<strong>limit(2) - </strong></code>optionally specifies how many to remove
  * <code>db.collection.drop()</code>- remove all records
* Mongoose
  * npm library used to manage mongoDB
  * Major steps
    * <code>mongoose.connect("mongodb://localhost/cat_app");</code>
    * Specify a schema to give it some structure, doesnt mean cannot add more later
      * <code>var catSchema = new mongoose.Schema({</code>

                ```
                    name: String,
                    age: Number,
                    temperament: String
    dateCreated: {type: Date, default: Date.now}
});
                ```

* <code>dateCreated: {type: Date, default: Date.now} -<strong> </strong></code>Gives it a default value, especially useful for dates or image placeholders
* Create a model out of it
  * <code>var Cat = mongoose.model("Cat", catSchema);</code>
  * After modelling we can use the variable to do <code>Cat.find(), Cat.remove(), Cat.insert(), Cat.update()</code>
  * <code>"Cat" </code>parameter is the singular version of what we are creating
* Inserting into db, can be done in 2 ways
  * Create a new object and save it
  * <code>var george = new Cat({</code>

                    ```
                        name: "George",
                        age: 11,
                        temperament: "Grouchy"
                    });

                    george.save((err, cat) => {
                        if(err) {
                            console.log("Something went wrong");
                        } else {
                            console.log("Successfully saved");
                            console.log(cat);
                        }
                    });
                    ```

  * `save()` takes a callback function
  * Do all in one step using `create({object}, callbackFunction)`
    * `Cat.create({ \
    name: "CatName" \
    age: 14, \
    temperament: "nice" \
}, (err, cat) => {...});`
    * When using BodyParser, we can specify the HTML input field to be `name="cat[name]",`then we can just put `Cat.create(cat);`
      * Note that **only <code>cat[name] </code></strong>is allowed, not <code>cat.name</code> or <code>cat['name']</code>, this is a bodyParser specific syntax.
* Find objects - takes 2 param, the first object is what to search for, second is the callback
  * <code>Cat.find({}, (err, cat) => {...});</code>
  * Associations
    * Embed
* <code>var userSchema = new mongoose.Schema({</code>

                ```
                    email: String,
                    name: String,
                    posts: [postSchema]
                });
                ```

* Put schema into the array
        *Reference
            *   `var userSchema = new mongoose.Schema({`

                ```
                    email: String,
                    name: String,
                    posts: [
                        {
                            type: mongoose.Schema.Types.ObjectId,
                            ref: "Post"
                        }
                    ]
                });
                ```

* Instead of storing an array of objects, we are storing an array of ObjectIds belonging to type Post
* When retrieving, if we just did normally we will get array of ObjectIds, but we want the actual objects. So
* `User.findOne({ name: "Bob Thurthur" }).populate("posts").exec((err, foundUser) => {`

                ```
                    if(err) console.log(err);
                    else console.log(foundUser);
                });
                ```

  * `populate` will fill the array with the actual posts
  * After `exec,`
  * `foundUser` is then the return object with Post objects
    * When to use which?
* `module.exports`
  * Is like the return statement of a file. The line that you export will be assigned to what is before the `require(..)` in another file
  * In models/user.js
    * `module.exports = mongoose.model("User", userSchema);`
  * In app.js
    * `var User = require("./models/user.js");`

# Docker

* [Git Repo](https://github.com/chongzixin/YelpCamp)
* Create Dockerfile
  * It’s a file that tells the container what files to run
  * Run `docker build -t yelpcamp .`to create image
* In cases when multiple services are required, e.g. MongoDB
  * Create `docker-compose.yml`
  * Run `docker-compose up`

# ElasticSearch

* Git Repo
* Analogy
  * MySQL => Databases => Tables => Columns/Rows
  * Elasticsearch => Indices => Types => Documents with Properties
    * E.g. SubaruFactory => Cars => Imprezza
  * [http://localhost:9200/[index]/[type]/[operation](http://localhost:9200/[index]/[type]/[operation)]
    * E.g. [http://localhost:9200/Cars/Imprezza](http://localhost:9200/Cars/Imprezza)
* Indices are both logical and physical separation
  * Each index is also stored as a shard, which then makes a difference to performance based on querying needs

# RESTful Routes

<table>
  <tr>
   <td><strong>Name</strong>
   </td>
   <td><strong>URL</strong>
   </td>
   <td><strong>Verb</strong>
   </td>
   <td><strong>Description</strong>
   </td>
  </tr>
  <tr>
   <td>Index
   </td>
   <td>/dogs
   </td>
   <td>GET
   </td>
   <td>Show list of dogs
   </td>
  </tr>
  <tr>
   <td>New
   </td>
   <td>/dogs/new
   </td>
   <td>GET
   </td>
   <td>Show form to create dogs
   </td>
  </tr>
  <tr>
   <td>Create
   </td>
   <td>/dogs
   </td>
   <td>POST
   </td>
   <td>Insert dog to DB
   </td>
  </tr>
  <tr>
   <td>Show
   </td>
   <td>/dogs/:id
   </td>
   <td>GET
   </td>
   <td>Show info of one dog
   </td>
  </tr>
  <tr>
   <td>Edit
   </td>
   <td>/dogs/:id/edit
   </td>
   <td>GET
   </td>
   <td>Show form to edit dogs
   </td>
  </tr>
  <tr>
   <td>Update
   </td>
   <td>/dogs/:id
   </td>
   <td>PUT
   </td>
   <td>Updates a dog, then redirect
   </td>
  </tr>
  <tr>
   <td>Destroy
   </td>
   <td>/dogs/Lid
   </td>
   <td>DELETE
   </td>
   <td>Deletes a dog, then redirect
   </td>
  </tr>
</table>

* A way to link HTTP requests with CRUD operations
* **Important** to put /new before /:id, otherwise /new will never work because it will also be interpreted as /:id
* HTML form doesnt support PUT and DELETE request, so will need to use `method-override`, which is basically a node library that adds `_method=PUT` to URL
  * `npm install method-override`
  * <code>&lt;form class="ui form" action="/blogs/&lt;%=blog.id%><strong>?_method=PUT</strong>" method="POST"></code>

# Swagger

* swagger-jsdoc vs swagger-express-generator

# Async foundations

* Stack
  * code gets pushed onto the stack when it starts executing, and pops when it is returned.
  * The top of the stack trace is the line number and function that it is currently running, whereas the bottom is where it started (which is usually `main`)
* Heap
  * memory gets set aside in the heap when an object is created
  * During reassignment only a reference is stored.
    * `var obj = [1,2,3]; // created`
    * `var ref = obj; // reassigned, only stores reference`
* Queue and Event Loop
  * Queue is async items that are waiting to be run
  * Event Loop puts items on the Queue into the stack when the stack is empty
  * In setTimeout, the callback function is first placed in the queue. Once the main function returns, the stack becomes empty and the Event Loop puts the callback into the stack.
    * <code>setTimeout(function, <strong>0</strong>)</code> - “0” doesnt mean the function runs immediately, it is only run after the main function returns
* Promises
  * Something that will happen in the future, and we can determine what to do when each scenario happens. <code>resolve</code> calls the <code>.then</code>, <code>reject</code> calls the <code>.catch</code>
    * <code>var p1 = new Promise(function(resolve, reject) {</code>
    * <code>    var num = Math.random();</code>
    * <code>    if(num &lt; 0.5) resolve(num);</code>
    * <code>    else reject(num);</code>
    * <code>});</code>
    *
    * <code>p1.then(function(result) {</code>
    * <code>    console.log("Success: " + result);</code>
    * <code>});</code>
    *
    * <code>p1.catch(function(result) {</code>
    * <code>    console.log("Error: " + result);</code>
    * <code>});</code>
  * Promises chaining
    * Each <code>.then</code> returns another <code>Promise (thenable)</code>, making them chainable
    * Imagine if we wanted to setTimeout only after another timeout has finished. We will then be chaining multiple callbacks
    * Basically involves the use of multiple <code>.then</code> functions, and they will be run in order
  * <code>Promise.all</code>
    * Accepts an <strong>array</strong> of promises and resolves all of them, or rejects once one of them fail
    * If all passes, it will return an array of values from the pass-ed in promises
      * No guarantee that it will return in the same order
    * <code>Function getMovie(title) { return $.getJSON(...) } \
var titanicPromise = getMovie("titanic"); \
var shrekPromise - getMovie("shrek"); \
 \
<strong>Promise.all([titanicPromise, shrekPromise]).then(function(movies) {</strong> \
    return movies.forEach(value => console.log(value.Year); \
});</code>
  * AJAX
    * <code>XHR</code> (<code>XMLHttpRequest</code>) response text returns a string, so need to use <code>JSON.parse</code>
    * <code>fetch </code>- allows streaming so you don’t have to wait till the entire response is back before you start. More importantly, cleaner syntax.
      * <code>fetch(url).then().catch()</code>
      * All <code>.then()</code> returns promise objects
        * Can be converted into json by doing
          * .then(function(res) {  \
    return res.json().then(function (data) {  \
      data.results[0];  \
    }); \
}
      * Fetch is not supported by IE
    * <code>jQuery</code>
      * <code>$.ajax </code>is same as<code> jQuery.ajax - $ == jQuery</code>
      * <code>$.ajax, $.get, $.post, $.getJSON</code> - latter 3 uses <code>$.ajax</code> under the hood
      * <code>$.ajax().done().fail() - </code>automatically caters to completion and failure without needing to check.
      * $.ajax intelligently guesses return based on mimetime and parses it into an object - don’t have to do .json().then() unlike in fetch
      *
    * <code>Axios</code>
      * Lightweight library that builds on top of XMLHttpRequest. Supports node too.
      * <code>axios.get().then().catch()</code>
      * In error handling, can differentiate between request and response problems by looking at<code> err.response </code>and<code> err.request</code>
* Also found in [ES2017](#heading=h.orh8h9p3yk65)

# Advanced Array functions

* `Map`
  * Creates a new array, iterates through it, runs a callback on each value, adds the result to the new array
  * **Map always returns an array of the same length**
  * Callback function in map must always `return`
* `Filter`
  * Creates a new array, iterates through it, runs a callback, adds result to the new array if callback evaluates true
  * Result of callback is always evaluated into a boolean
  * Try not to use if statements in here, just write an expression
  * Useful if we want to return an array and take values out of it
* `Some`
  * Iterates through array, runs a callback, returns true for at least one single value returns true
  * Result of `some` is always evaluated to a boolean
* `Every`
  * Iterates through array, runs a callback, returns false for at least one single value returns false
  * Result of `every` is always evaluated to a boolean
* `Reduce`
  * Used to return an array into something else like a string or integer
  * Accepts a callback and an optional second parameter
  * Iterates through array, runs callback, first callback param is either first value of array or the optional second param, first param is called accumulator and return value becomes new value of accumulator. **Whatever is returned from the callback becomes the new value of the accumulator.**If no value is returned, it becomes undefined which will be a problem
  * callback(accumulator, nextValue, index, array)
  * Common Use Cases
    * Sum up values in an array.
    * Put together multiple strings
      * [name1, name2, name3].reduce(function(...) { \
    return accumulator += ‘ ‘ + nextValue; \
}, “The instructors are’);
    * Make array into key-value pair with count
      * Use`if(nextValue in accumulator)`to check if key exists
    * Sum odd numbers
    * Create array of full names from array of object { firstName, lastName }

# Closures, this

* Closures
  * Function that makes use of variables defined in outer functions that have previously returned
    * `function outer() { \
    var start = "Closures are"; \
    return function inner() { \
        return start + " " + awesome; \
    } \
} \
 \
outer(); // will return the inner function \
outer()(); // will return "Closures are awesome"`
    * **inner function must have a return, and inner function must use variables from outer function**
    * Inner function can be anonymous, but useful to be named esp during debugging
  * Common Uses
    * Private variables in OOP
      * Conceptually, return a copy of the variable instead of the actual so that it cannot be modified
* `this`
  * Two reserved keywords in a function - `arguments` and `this`
  * Value is determined using four rules
    * `Global`
      * When not attached, it refers to global context which is `window`
    * `object/implicit`
      * If `this` is found inside a declared object, this will refer to the nearest parent object only when a function is run
    * `Explicit - call(), apply(), bind()`
      * <code>var person = { \
    firstName: "Colt", \
    dog: { \
      sayHello: function() { \
          Return "Hello " + this.firstName; \
      }, \
} \
person.dog.sayHello(); // returns undefined because this.firstName refers to dog and not person due to <strong>implicit binding</strong>.</code>
      * <code>person.dog.sayHello.call(person); // means that this in sayHello refers to person. </code>
      * The above is resolved by using call, apply, bind - their first param determines what <code>this</code> should reference to.
        * They can only be used by functions, not by objects, string etc.

<table>
  <tr>
   <td>
<strong>Name of method</strong>
   </td>
   <td><strong>Parameters</strong>
   </td>
   <td><strong>Invoke immediately</strong>
   </td>
  </tr>
  <tr>
   <td>call
   </td>
   <td>thisArg, a, b, c, d, ...
   </td>
   <td>Yes
   </td>
  </tr>
  <tr>
   <td>apply
   </td>
   <td>thisArg, [a,b,c,d,...]
   </td>
   <td>Yes
   </td>
  </tr>
  <tr>
   <td>bind
   </td>
   <td>thisArg, a, b, c, d, ...
   </td>
   <td>No
   </td>
  </tr>
</table>

* `call()`
  * Common use cases
    * Prevents repeating of code
      * `function sayHi() { return this.firstName; } \
var jack = { firstName: "jack" }; \
var john = { firstName: "john" }; \
sayHi.call(jack);`
    * Change array like objects into arrays
      * `var divs = document.getElementsByTagName("div"); // divs is not an array \
var divsArray = [].slice.call(divs); // will change divs into an array`
* `apply()`
  * Common use cases
    * Passing an array into a function that only accepts list
      * `var nums = [5,16,7,2,46]; \
Math.max(nums); // returns NaN \
Math.max.apply(this, nums); // returns 46`
    * Passing an array into a function that accepts separate arguments
      * `function sumValues(a,b,c) { return a+b+c; } \
var values = [1,2,3]; \
sumValues(values); // incorrect \
sumValues.apply(this, values); // 6`
* `bind()`
  * Returns a function with the keyword this bind to the first param so that it can be called later
  * Common use cases
    * Park for later use
      * `function addNumbers(a,b,c,d) {  \
    return this.firstName + " just calculated " + (a+b+c+d); \
} \
var elie = { firstName: "elie" }; \
var elieCounts = addNumbers.bind(elie, 1,2,3,4); \
elieCounts(); // returns "elie just calculated 10"`
    * Partial application (e.g. when we dont know all our arguments upfront)
      * `var elieCounts = addNumbers.bind(elie, 1,2); \
elieCounts(3,4); // returns "elie just calculated 10"`
    * Asynchronous functions
      * <code>var colt = { \
    firstName: "colt", \
    sayHi: function() { \
        setTimeout(function() { \
            console.log("Hello " + this.firstName); \
        }<strong>.bind(this)</strong>, 2000); \
    } \
}</code> \
 \
<code>this.firstName</code> refers to global context because it’s in async function \
Adding <strong><code>.bind(this)</code></strong> will bind <code>this.firstName</code> to the colt object.
    * <code>New</code>
      * Create a new object. Inside function definition, <code>this</code> refers to the object in which it was created with <code>new</code>
  * <code>"use strict"</code>
    * Used to ensure that global variables are not created unintentionally when assigning variables without declaring in functions

# Single Page Apps with jQuery

* Adding event listener to list items that are updated on the fly - e.g. Todo list
  * Instead of listening on the individual list items, we want to listen on specific tags of the list itself
  * If this span is in a list item, we want to make sure that it does not affect event listeners on the &lt;li>, so use stopPropagation - known as event bubbling
  * `$('list').on('click', 'span', function(e) { \
    e.stopPropagation(); \
});`

# Frontend Frameworks

* Javascript libraries that handle DOM manipulation
* State Management - frameworks provide tools to auto track
* Server returns bundle.js (contains React, ReactDOM, custom js), and React now takes control of the DOM

# React

* View library
* Common libraries - ReactRouter, Redux
* Composable Components
  * Every component will `extends React.Component`and have`render()`
* `JSX with Babel`
  * `Transpiler to convert from JSX to Vanilla JS`
  * `JSX allows us to write ReactDOM code in HTML`
  * To use CSS, must use <code>&lt;div <strong>className="card"</strong>> </code>instead of <code>class</code>
  * Everything is JS object
  * put them into curly braces for it to be evaluated
  * Inline styles will look like &lt;div style=<strong>{{fontSize: “20em”}}</strong>>
    * First {} to evaluate JS
    * Second {} because it should be put into object
    * “” because this is JS object and not CSS
* Use map to render list of components
  * <code>const hobbies = ["eating", "drinking", "sleeping"]; \
… \
return ( \
    &lt;ul> \
<strong>        {hobbies.map( (h,i) => {</strong> \
<strong>            return &lt;li key={i}>{h}&lt;/li></strong> \
<strong>        })} \
…</strong></code>
  * map is commonly used here because it returns array
  * JSX components will need an iterator
* Returning a component within another
  * <code>class HobbyList extends React.Component { \
  return (&lt;ul>...&lt;/ul>); \
} \
class Pet extends React.Component { \
  return ( \
      &lt;div>...&lt;/div> \
<strong>      &lt;HobbyList /></strong> \
  ); \
}</code>
  * Can just use the HobbyList like it’s a tag

### Create React App

* Webpack
  * Bundler to combine different JS files into a bundle.js
  * Has a plugin system to run babel - so that code is converted to vanilla before sending to client
* `npm install -g create-react-app`
  * `create-react-app helloworld`
  * `npm start`
* By default, the current create-react-app uses functions, to use the old classes, run `create-react-app [Project Name] --scripts-version 2.0.3`
* Export default vs non default export
  * `App.js // old create-react-app, new one uses class`
    * <code>import <strong>React, { Component }</strong> from 'react';</code>
    * <code>React </code>- default export
    * <code>{ Component } </code>is in <code>{}</code> because it’s a non-default export
    * <code>export default App</code>
  * <code>Index.js</code>
    * <code>import App from "./App";</code>
    * When importing a <code>export default </code>component, we can then change to any name like <code>Pizza</code>. Then we can just use <code>&lt;Pizza /></code>
    * If want to use Pizza with non-default export,<code> import { App as Pizza } …</code>
* Pet.css should only relate to Pet.js component
  * In Pet.js, <code>import './Pet.css';</code>

### Props

* Immutable data passed to components accessible using `this.props`
  * <code>&lt;NewComponent  \
<strong>    text="this is a prop" </strong> \
/> \
... \
render() { return &lt;div><strong>{this.props.text}</strong>>/div> };</code>
  * <code>Never ever change props</code>
* <code>defaultProps</code>
  * Specify what are default props when it is not specified
  * <code>class IngredientList extends Component { \
<strong>    static defaultProps = { \
        ingredients: [] \
    }</strong> \
 \
    render() {...}  \
} \
 \
// alternatively, specify outside the class \
<strong>IngredientList.defaultProps = { \
    ingredients: [] \
};</strong></code>
  * <code>In another example</code>
    * <code>App can have array of recipes as defaultProps</code>
    * <code>App.render() { \
  return ( \
    &lt;div> \
      {this.props.recipes.map((r,index) => { \
<strong>        &lt;Recipe key={index} title={r.title} ing={r.ing} img={r.img}> /> \
        // can be done using rest operator too, but need to be clear what props \
        &lt;Recipe key={index} {...r} /></strong> \
      })} \
    &lt;/div> \
  ) \
}</code>
* <code>propTypes</code>
  * A contract that says what props must be defined when a component is used
  * Used only in development mode.
  * Install with <code>npm install --save prop-types</code>
  * <code>static propTypes = { \
    // specifies the ingredients is mandatory and need to be an array of strings \
    ingredients: <strong>PropTypes.arrayOf(PropTypes.string).isRequired</strong> \
}</code>
* <code>props.children</code>
  * Collection of the children inside of a component

### State

* Stateful data, data in application that can change (unlike props)
* Every constructor will take props and call its superclass. \
<code>class App extends Component { \
    <strong>constructor(props) { \
        super(props); \
        this.state = { favColor: "red" }; \
    } \
 \
    </strong>render() { return this.state.favColor } \
}</code>
* <code>this.setState({ }, callback);</code>
  * Send in a new object to use.
  * Do not add or modify state object directly. MUST USE <code>setState</code>
  * Is an async method that will eventually invoke <code>render()</code>
  * Use the callback function to get notified when state is updated
* Pure function
  * Function with no side effects, does not modify its inputs.
  * Repeatable such as same inputs will give same outputs
  * Always give it a new object
* Some rules
  * Whenever a setState depends on previous state, use a function as the first parameter to setState
  * setState is async, so setting a console.log on state will not change immediately, use callback function

### React Component Architecture

* State is always passed from a parent down to child component as prop. State should never be passed to sibling or parent
* In a TicTacToe example, if we needed a reset button on the navbar that will restart the state of TicTacToe, then the state of the board will have to be stored in App.:- \
`&lt;App> \
    &lt;NavBar /> \
    &lt;TicTacToe /> \
&lt;/App>`
* Never assign a prop to a state. Usually means something wrong.
* Stateless Functional Component
  * Components implemented using function, not class. The function then implements the render method only, no constructor and no state.
  * New react-app uses this
  * `import React from 'react'; \
const Greeting = props => ( &lt;h1> Hello, {props.name} &lt;/h1> ); \
export default Greeting`

### Virtual DOM

* After doing setState, reconciliation handles updates to the DOM
* Synthetic events - consistent API on all browsers for event handling
* React 16 changes
  * Render can return an array of JSX elements (i.e. dont have to create a top level element just for this)
  * Error Boundary
  * Fiber as a reconciliation engine

### Events

* Can specify a callback function inside
* <code>render() { \
  return ( \
    &lt;div> \
      …. \
      <strong>&lt;button type="button" onclick={() => this.setState({name: "TIM"})}>&lt;/button></strong> \
… \
}</code>
* Alternatively, specify the method outside of render
* <code>constructor(props) { \
  … \
  <strong>this.handleClick = this.handleClick.bind(this); // without this binding, this.setState in handleClick will not refer to this class.</strong> \
}<strong> \
 \
handleClick(e) { \
  this.setState((prevState, props) => ({ \
    name: prevState.name.toUpperCase() \
  }); \
}</strong> \
render() { \
  ... \
  &lt;button type="button" onclick=<strong>{this.handleClick}</strong>> // note that it's not handleClick<strong>()</strong> \
}</code>

### Forms

* Uncontrolled component - React is not aware of what user types
  * `&lt;input type="text"/>`
* Controlled component - React is in control of state because of onChange
  * Specifying name is important so that we can use `e.target.name` and link it with `e.target.value`
  * <code>&lt;input type="text" value={this.state.inputText} name="inputText" \
  <strong>onChange={(e) => { \
    this.setState({ [e.target.name]: e.target.value }); \
  }}</strong> \
/></code>
* Form submit
  * <code>&lt;form <strong>onSubmit</strong>={(e) => { \
  e.preventDefault(); // prevents default behaviour of submitting app and losing all data \
  const data = [...this.state.data, this.state.inputText]; \
  this.setState({data, inputText: ''}); \
}}></code>
  * Don’t use submit button and onclick because a lot of behaviours don't get captured.
* If a form is supposed to update state of another component, we do this using callbacks.
  * E.g. RecipeInput is form, RecipeApp contains state. RecipeInput will do a callback to function specified in RecipeApp

### ref

* Direct reference to DOM element - as compared to through state
* Should be last resort when you cannot do through React
* Use case
  * Animations, 3rd party DOM libraries, manage focus, text selection or media playback

# React Native

* Component
  * Build custom components based on React Native native components
  * Styling uses Inline Styles or Stylesheet Objects
    * No CSS, though most of it look alike
  * Must use `&lt;Text>` component to display text
  * `&lt;View>`’s main job is to configure the look of the view using stylesheets
  * `&lt;ScrollView>` adds a scroll view, but can be inefficient because it’s preloaded
  * Use `&lt;FlatList>` to do this more efficiently.
    * data is the array of items, renderItem takes a function of what to display for each item

            ```
            <FlatList
                    data={goalList}
                    renderItem={itemData => (
                      <View style={styles.goal_item}>
                        <Text>{itemData.item}</Text>
                      </View>
                    )}
                  />
            ```

* Custom components don’t have onPress (etc.) event handlers
  * Solved by nesting it within a `&lt;Touchable>` such as `&lt;TouchableOpacity>`
* Styles
  * Every view by default uses `Flexbox,`and by default organises child elements by column (i.e. top to bottom)
  * To change, add `FlexDirection: "row",`can also reverse direction by setting it to`"row-reverse"`
  * Child elements in flexbox align themselves according to cross-axis
    * `justifyContent` aligns on main-axis
    * `alignItems` aligns on cross-axis
  * By default, `View` only takes as much space as the child element require, but by adding `flex: 1` to the child element, it will now take as much space it can get on the main-axis
    * flex:1 is a common style to apply to the base view (typically styled as screen)
  * Inline style are properties defined as part of the component
    * <code>&lt;View style=<strong>{{</strong>flex:1<strong>}}</strong>> // first {} is React syntax to interpret object, second {} is because it's actually a javascript object</code>
  * Stylesheet objects are defined elsewhere, and put into the component properties
    * &lt;View style={styles.buttonStyle}>
    * Uses <code>Stylesheet.create()</code>, though it can also be a standard javascript object. But there could be other benefits in future by using <code>create()</code>, so no harm doing so now. It also has built-in validation.
  * <code>&lt;Text></code> has much lesser styles compared to <code>&lt;View></code>, so we can style this by nesting <code>&lt;Text></code> within another <code>&lt;View></code>
    * <code>{goalList.map((goal) => <strong>&lt;View style={styles.goal_item}></strong>&lt;<span style="text-decoration:underline;">Text</span> key={goal}>{goal}&lt;/<span style="text-decoration:underline;">Text</span>><strong>&lt;/View></strong>)}</code>
* Creating reusable style components
  * <code>&lt;View style={<strong>{...styles.card, ...props.style}</strong>}><strong>{props.children}</strong>&lt;/View></code>
  * <strong><code>{...styles.card, ...props.style} - </code></strong>merges everything from <code>props.style</code> and <code>styles.card</code> into a new object, at the same time overriding the repeated ones.
  * <strong><code>{props.children}</code></strong>
  * We can also forward all the props from the main class to the component class by setting <code>{...props}</code>, note in the below example style will be overridden because it’s specified.
    * <code>&lt;TextInput <strong>{...props}</strong> style={{...styles.textInput, ...props.style}} /></code>

## Fonts

* Loading fonts or images using `&lt;AppLoader>`
  * startAsync must take an async function that returns a promise, and we must provide another function onFinish so that it moves on from the loading screen
  * `const fetchFonts = () => {`

            ```
              return Font.loadAsync({
                'open-sans': require('./assets/fonts/OpenSans-Regular.ttf'),
                'open-sans-bold': require('./assets/fonts/OpenSans-Bold.ttf');
              });
            }

...
<AppLoading startAsync={fetchFonts} onFinish={() => setDataLoaded(true)} />
            ```

* Using the fonts globally
* Because this is Javascript and not CSS, fonts are not “inherited” when it is specified in the “parent” component (except when it comes to `&lt;Text>`)
* 2 solutions
  * The solution is to create a new component and wrap everyone within it.
  * Create a default stylesheet and reference that in all places that need it

## Images

* Local images uses require() to reference the image
  * `&lt;View style={styles.imageContainer}>`

        ```
        <Image
        style={styles.image}
        source={require('../assets/success.png')}
        resizeMode='cover'
        />
        </View>
        ```

* Network images
  * Same as above, but specifies source with uri property
    * **<code>source={{uri:'https://image.url'}}</code></strong>
  * Images coming from network MUST always have width and height property

## Text

* Does not use Flexbox - so text is automatically wrapped into new lines.
* Styles are inherited

## Switch

* Have to manually manage state with useState

## Icons

* `import { Ionicons } from '@expo/vector-icons';`

## React Hooks

* `useRef`
  * Like useState, this value is sustained even when the component is re-rendered
  * Difference between this and useState is that when you change the value of useRef, the component does not re-render
  * Has `.current` to reference current value
* `useEffect(callbackFunction, arrayOfDependencies)`
  * Allows you to run logic after every render cycle - usually used to check business logic
  * First parameter is a function that runs whenever the component is re-render
  * Second parameter is an array of items that you want to watch for to determine if the effect should run. It helps with performance.
* `useCallback(callbackFunction, arrayOfDependencies)`
  * Wrap this around functions that we don’t want to recreate whenever the component renders. This is often used with useEffect because useEffect usually have inner functions that are dependencies. And inner functions always get rebuilt when component rebuilds.
  * Useful for gathering states of a multi-filter page, or **when passing params from functional components to navigation objects**

## Navigation

* Use react-navigation library
  * `import { createStackNavigator } from 'react-navigation-stack';`
  * `import { createBottomTabNavigator } from 'react-navigation-tabs';`
  * `import { createDrawerNavigator } from 'react-navigation-drawer';`
* Top-level screens that are referenced in `createStackNavigator()` automatically get a `navigation` object in their props
  * We can then use it by calling <code>props.navigation.navigate({<strong>routeName</strong>: 'CategoryMeals'});</code>
    * where <code>routeName</code> points to the key in the Navigator file
  * <code>push() </code>does the same thing too, <strong>and also allows you to navigate to the current page </strong>(which can be useful in a Files app where we keep reusing the same folder page).
  * <code>goBack()/pop() </code>lets the user go back to the previous screen, same as BACK button at the top left.
    * <code>pop()</code> is only available on a StackNavigator
  * <code>popToTop()</code> brings back to root screen
  * <code>replace()</code> replaces the screen on the stack. This is useful for login screen because you dont want the user to go back
* When using react-navigation library, each screen can then define navigationOptions object to specify styles
  * <code>CategoriesScreen.navigationOptions = {</code>

        ```
            headerTitle: 'Meal Categories',
            headerStyle: {
                backgroundColor: Platform.OS === 'android' ? Colors.primaryColor : '',
            },
            headerTintColor: Platform.OS === 'android' ? 'white': Colors.primaryColor,
        };
        ```

* Default navigation options can also be provided to `createStackNavigator()` as the second parameter (for all default options) so that the same style applies
  * They will always be overridden
* Passing params
  * On main screen: <code>props.navigation.navigate({routeName: 'CategoryMeals', <strong>params: {key:value}</strong>);</code>
    * Can pass multiple IDs
  * On receiving screen
    * If within component and can use props: <code>const catId = props.navigation.getParam('categoryId');</code>
    * Otherwise, navigationOptions can also take a function, but have to return the same object
    * <code>CategoryMealsScreen.navigationOptions = <strong>navigationData</strong> => {</code>

            ```
                const catId = navigationData.navigation.getParam('categoryId');
                const selectedCategory = CATEGORIES.find(cat => cat.id === catId);

                return {
                    headerTitle: selectedCategory.title,
                };
            }
            ```

* Drawer Navigator
  * This is usually the main navigator, because it will show screens that are also not in the bottom tabs
  * After declaring it, you will also need to use declare them as HeaderButtons on the screens that you want to show the drawers for
  * After showing the icon, you will need to define the function that can display this drawer (this can be found in the navigation prop)
* Passing data between Component and Navigation Options (e.g. when you press SAVE and you want to change the state)
  * Use setParams

## Redux

* Packages
  * react-redux
  *
* Central store for entire application (e.g. is a user logged in) in **memory**
* Reducers update Central Store, and can trigger updates to components who subscribe to it.
* Base structure of reducer
  * When Redux starts, it will automatically call in initial action, so we have to set the initial state
  * `const initialState = {`

            ```
                meals: MEALS,
                filteredMeals: MEALS,
                favouriteMeals: [],
            };

            const mealsReducer = (state = initialState, action) => {
                return state;
            };

            export default mealsReducer;
            ```

* Connecting it in App.js
  * `import { createStore, combineReducers } from 'redux'; \
import { Provider } from 'react-redux'; \
 \
// merge all the reducers into a single one`

        ```
        const rootReducer = combineReducers({
          meals: mealsReducer,
        });
        const store = createStore(rootReducer);

// then wrap Provider around the main component returned by App.js
export default function App() {
  …
  return (
            <Provider store={store}>
              <MealsNavigator />
            </Provider>
          );
        };
        ```

* Reading data from the store
  * Can only be used inside of functional components (e.g. `CategoryMealsScreen`)
  * `const availableMeals = useSelector(state => state.meals.filteredMeals);`
  * `useSelector`takes a function with state`parameter`
  * We retrieve the reducer we want out of this state. (e.g. `state.meals`where` meals `is the mealReducer as above)
  * We can then refer to the object we want based on the state in the reducer `(e.g. state.meal.filteredMeals)`
* Writing/updating data in the store
  * Write the action
    * `export const TOGGLE_FAVOURITE = 'TOGGLE_FAVOURITE';`

            ```
            export const toggleFavourite = (id) => {
                return {
                    type: TOGGLE_FAVOURITE,
                    mealId: id
                };
            };
            ```

  * Specify how the reducer will use the action
    * The pattern here is to use a switch case to check against what action type it is, in our case we will just add or remove an item from the favourites list depending on whether it was already inside. **Note that we always return a new copy of the state**
    * `const mealsReducer = (state = initialState, action) => {`

            ```
                switch(action.type) {
                    case TOGGLE_FAVOURITE:
                        const existingIndex = state.favouriteMeals.findIndex(meal => meal.id === action.mealId);
                        if(existingIndex >= 0) {
                            const updatedFavMeals = [...state.favouriteMeals];
                            updatedFavMeals.splice(existingIndex, 1);
                            return { ...state, favouriteMeals: updatedFavMeals};
                        } else {
                            // the item is not inside, so just add it to favourites. start by getting the meal object first
                            const meal = state.meals.find(meal => meal.id === action.mealId);
                            return { ...state, favouriteMeals: state.favouriteMeals.concat(meal)};
                        }
                    default:
                        return state;
                }
            };
            ```

  * Dispatching the action
    * `setFilters()` is the action we created in the `actions/meal.js`, appliedFilters is the params we give it
    * `const dispatch = useDispatch(); \
... \
dispatch(toggleFavourite(id));`

## Native Functionality

*

## Alternatives to fully-managed Expo

<table>
  <tr>
   <td><strong>Expo managed workflow</strong>
   </td>
   <td><strong>Expo barebones</strong>
   </td>
   <td><strong>React Native Pure</strong>
   </td>
  </tr>
  <tr>
   <td>Wrapper class with lots of packages.
   </td>
   <td>In between the two. Equivalent to using React Native Pure but with <a href="https://docs.expo.io/bare/existing-apps/">Expo SDK</a>
   </td>
   <td>Works by compiling code into native code and allows direct access to native code.
   </td>
  </tr>
  <tr>
   <td><strong>Pros</strong>
<ul>

<li>Lots of packages

<li>Easy to set up (no XCode and Android Studio required)
</li>
</ul>
   </td>
   <td><strong>Pros</strong>
<ul>

<li>Can use all the expo packages

<li>Can use native modules too
</li>
</ul>
   </td>
   <td><strong>Pros</strong>
<ul>

<li>Can connect to native modules

<li>Slightly better performance
</li>
</ul>
   </td>
  </tr>
  <tr>
   <td><strong>Cons</strong>
<ul>

<li>Slight performance with expo wrapper

<li>Cannot connect native modules
</li>
</ul>
   </td>
   <td>
   </td>
   <td><strong>Cons</strong>
<ul>

<li>More manual configuration to do
</li>
</ul>
   </td>
  </tr>
</table>

# TypeScript

[https://learncsc.udemy.com/course/understanding-typescript/learn/lecture/16949812#overview](https://learncsc.udemy.com/course/understanding-typescript/learn/lecture/16949812#overview)

* Basics
  * Browsers can’t execute it
  * Write in TypeScript, but it gets compiled into JavaScript through “workarounds”
  * More strict typing where code gets caught at compile time instead of runtime
  * Compile with `tsc &lt;filename.ts>`
* Types
* Core Types
  * `number, string, boolean, object, Array, Tuple, enum, any`
  * Always in lowercase
  * Typescript can enforce that an object always has certain properties
  * `Tuple` is a fixed length array
* Union Types
  * Used to overload a method to take in different data type
  * <code>function combine(input1: <strong>number | string</strong>, input2: <strong>number | string</strong>) {</code>

            ```
                let result;
                if(typeof input1 === 'number' && typeof input2 === 'number') {
                    result = input1 + input2;
                } else {
                    result = input1.toString() + input2.toString();
                }
                return result;
            }
            ```

* Literal Types
  * Used to specify exactly what value we want to accept
  * `function combine(`

            ```
                input1: number, 
                input2: number, 
                resultConversion: 'as-number' | 'as-text'
            )
            ```

* Alias Type
  * Create a new “variable” with a `type` at the top
  * **<code>type Combinable = number | string;</code></strong>

            ```
            type ConversionDescriptor = 'as-number' | 'as-text';

            function combine(
                input1: Combinable, 
                input2: Combinable, 
                resultConversion: ConversionDescriptor
            )
            ```

* Function Return type
  * <code>function add(n1: number, n2: number): <strong>number</strong> {}</code>
  * <code>function print(text: string): <strong>void</strong> {}</code>
* <code>unknown </code>- quite similar to <code>any</code>, but <code>unknown</code> requires explicit checking or it will throw an error
* <code>never</code> - quite similar to <code>void</code>, but <code>never</code> does not even return undefined. Useful for error functions
* Compiler
  * <code>tsc app.ts <strong>--watch</strong></code> to constantly watch for changes for a single file
  * <code>tsc --init</code> to tell typescript that everything in the current folder is a single project
    * <code>tsconfig.json</code> will be created
    * Thereafter, running <code>tsc</code> command alone will automatically compile all files in that project
  * <code>tsconfig.json</code> tells compiler how to compile the files
    * <code>"exclude": ["analytics.ts"]</code> will tell the compiler to exclude this file from compilation
    * Most common to exclude “node_modules” because you dont want to compile typescript files in those modules. It is already the default
    * Other options include<code> "include": [], "files": []</code>
    * <code>"noEmitError": "true"</code> - stops emitting files when there are errors
    * <code>"noUnusedLocals": true, /*Report errors on unused locals.*/</code>
    * <code>"noUnusedParameters": true, /*Report errors on unused parameters.*/</code>
    * <code>"noImplicitReturns": true, /*Report error when not all code paths in function return a value.*/</code>
* Classes
  * Properties and parameters can be typed
  * When we send <code>this:Department</code> into a method, we also ensure that the object that is calling in is of class Department
  * <code>class Department {</code>

        ```
            private name: string;
            private employees: string[] = [];

            constructor(name: string) {
                this.name = name;
            }

            // by sending this:Department, we are forcing typescript to check that any object calling the describe method is actually fulfills a Department object
            describe(this: Department) {
                console.log("Department: " + this.name);
            }
        ```

        …

* Access modifiers - properties are defaulted to **<code>public</code></strong>
  * This is checked during compile time and not run time
* Shorthand - instead of specifying properties and then assigning them in the constructor. We can use the shorthand by specifying access modifiers and property names in the constructor. In the below example, <code>string id</code> and <code>string name</code> are also created
  * <code>constructor<strong>(private id: string, private name: string)</strong> { }</code>
* readonly modifier makes sure that the property cannot be changed after
  * <code>private <strong>readonly</strong> id;</code>
* Inheritance
  * <code>protected</code> keyword allows properties/methods to be accessible from subclasses
* Getter/Setter
  * Getter
    * Specified as a method within the class definition \
<strong><code>get mostRecentReport() {</code></strong>

                ```
                        if(this.lastReport) {
                            return this.lastReport;
                        }
                        throw new Error("No report found");
                }
                ```

    * But accessed like a property when in use \
<code>console.log(<strong>accounting.mostRecentReport</strong>);</code>
  * Setter
    * Also specified as method within class definition \
<strong><code>set mostRecentReport(value: string) {</code></strong>

                ```
                        if(!value) {
                            throw new Error("Please pass in a valid report");
                        }
                        this.addEmployee(value);
                }
                ```

    * Also accessed like a property when trying to use \
`accounting.mostRecentReport = "Report added via Setter";`
* `static`methods and properties
  * For utility methods, specified using the name of the class
* `abstract` - no parenthesis after, and must always have a return type
  * `abstract describe(this: Department): void;`
* `private` constructors - helpful for implementing Singleton by combining it with static method
  * `private static instance: AccountingDepartment;`

            ```
            private constructor(id: string, private reports:string[]) {
                    super(id, "Accounting");
                    this.lastReport = reports[0];
            }

            static getInstance() {
                    if(this.instance) 
                        return this.instance;

                    this.instance = new AccountingDepartment("d2", []);
                    return this.instance;
            }
            ```

* Interfaces
  * Used to show the structure
  * A class can implement multiple interfaces
  * `readonly` objects in interface ensures that you only set it once
  * Can inherit from **multiple** classes through `extends Interface1, Interface2`

        ```
        interface Named {
            readonly name: string;
            outputName?: string;
        }

        interface Greetable extends Named {
            greet(phrase: string): void;
        }
        ```

* Optional properties and parameters, add a`?` behind the name. E.g.
  * Classes can have optional properties and parameters in methods
  * Interfaces can have optional properties and methods (e.g. implementing class doesn’t need to define this method)
  * <code>optionalName<strong>?</strong> : string;</code>
  * <code>constructor(n<strong>?</strong>: string); // means that we can also have a no-argument constructor</code>
  * <code>add?(n1: number, n2: number): number</code>
* Advanced Types
  * Intersection Type
    * The intersection type will share overlapping properties, e.g. ElevatedEmployee below will have name, privileges and startDate.

            ```
            type Admin = {
                name: string;
                privileges: string[];
            }

            type Employee = {
                name: string;
                startDate: Date;
            }

            type ElevatedEmployee = Admin & Employee;
            ```

  * Type Guards
    * used by the compiler to protect against potential mistakes during union or intersection types
      * `typeof` protects native types
      * `in` protects custom types
      * `instanceof` protects classes
  * Discriminated Unions - a pattern that forces each type/interface/class to have a type. This is so that we can run a switch case separately to check their types. The beauty is that the compiler actually autocompletes a lot of the code when using this pattern
    * `interface Bird {`

            ```
                type: 'bird',
                flyingSpeed: number;
            }

            interface Horse {
                type: 'horse'
                runningSpeed: number;
            }

            type Animal = Bird | Horse;

            function moveAnimal(animal: Animal) {
                let speed;
                switch(animal.type) {
                    case 'bird':
                        speed = animal.flyingSpeed;
                        break;
                    case 'horse':
                        speed = animal.runningSpeed;
                        break;
                }
                console.log('Moving at speed: ' + speed);
            }
            ```

* Type Casting - 2 ways to show typecasting
  * <code>const userInputElement = <strong>&lt;HTMLInputElement></strong>document.getElementById('my-input');</code>
  * <code>const userInputElement = document.getElementById('my-input') <strong>as HTMLInputElement</strong>;</code>
  * The former <code>&lt;HTMLInputElement></code> may be more confused with React since JSX uses angle brackets too. So the latter using the <code>as</code> keyword is less ambiguous.
* Index Type

            ```
            interface ErrorContainer {
                // [prop: string] basically states that we don't know how many properties there will be, and what names they will have, we only know that they are of type string
                [prop: string]: string;
            }

            const errorBag: ErrorContainer = {
                email: 'Not a valid email!',
                username: 'Must start with a capital character!',
            }
            ```

* Function overloading - a function with the same name but takes different number of parameters and/or have different return types
  * **<code>function add_overloaded(a: number, b: number) : number;</code></strong>

            ```
            function add_overloaded(a: string, b: string) : string;
            function add_overloaded(a: number, b: string) : string;
            function add_overloaded(a: string, b: number) : string;
            function add_overloaded(a: Combinable, b: Combinable) {
                if (typeof a === 'string' || typeof b === 'string') {
                    return a.toString() + b.toString();
                }
                return a + b;
            }

            const result = add_overloaded('Max ', 'Brenner');
            result.split(' '); // this would have failed if not overloaded because typescript doesn't know that the above method will definitely return a string
            ```

* Optional Chaining - using ? to check if a nested object exists so that it doesnt throw runtime errors
  * **<code>console.log(fetchedUserData && fetchedUserData.job.title); // standard javascript way of ensuring that a variable is not null before accessing it to avoid runtime errors</code></strong>

            ```
            console.log(fetchedUserData?.job?.title); // in typescript, we just add question marks to variables we are unsure if exists
            ```

* Nullish Coalescing - if the value is not null or undefined, then we will use the fallback value specified after ??
  * `const userInput = '';`

            ```
            const storedData = userInput ?? 'DEFAULT';
            console.log(storedData);
            ```

* Generics

# Android

* `adb commands`
  * Force phone to go into doze for testing `adb shell dumpsys deviceidle force-idle`
  * Check which apps are on whitelist `adb shell dumpsys deviceidle whitelist`
  * Unplug battery to test`adb shell dumpsys battery unplug`
    * Reset `adb shell dumpsys battery unplug reset`
* Different ways to execute periodic jobs
  * Timer:
  * `timer.scheduleAtFixedRate(new TimerTask() {`

            ```
                        @Override
                        public void run() {
  // do something
            }}, 60000, 60000);
            ```

* Handler
* `Handler handler = new Handler();`

            ```
            handler.postDelayed(new Runnable() {
            public void run() {
              // do something
            }
            }, 5*60*1000);
            ```

*

# Testing

* Steps
  * Framework to write test
  * Describe code that we are testing
  * Tool to make assertions or expectations about code
* Jasmine
  * Works on both frontend and backend
  * Need to include js and css
  * Syntax
    * `describe("Earth", function() { \
    it("is round", function() { \
        expect(earth.isRound).toBe(true); \
    }); \
    it("is the third planet from the sun, function() { \
        expect(earth.numberFromSun).toBe(3); \
    }); \
});`
  * Each spec is a test
  * Matchers - functions that help to assert
    * `toBe / not.toBe`(uses ===)
    * `toBeCloseTo`
    * `toBeDefined`
    * `toBeFalsey / toBeTruthy`
    * `toContain`(useful for array)
    * `toEqual`(uses ==)
  * `BeforeEach / AfterEach`
    * Code in this block is run before/after each test is run, useful for variable init - because of scoping, be sure to declare variables outside the beforeEach block
    * afterEach useful for tear down or resetting variables to original state before next test
  * describe can be nested for proper organisation
  * Pending
    * These tests dont get run, and can be declared in 3 ways
    * `xit`
    * Don’t specify callback
    * Use `pending();` while in the function
  * Spies
    * Spies are jasmine’s version of mock. Mock is like a fake object and function
    * Useful to test if
      * a function has been called (e.g. connect to database)
      * What arguments it’s called with
      * How many times was it called
  * Clocks
    * Used to test async code, and others like SetTimeout and SetInterval
    * Be sure to uninstall to restore it to original functions
    * For async functions, pass `done()`to the callback function of `it` so that it will know when the async function has ended.
* Types of test
  * Unit Tests
    * TDD (Test Driven Development) asks to write tests first, then write the code to pass the test. Arguably better quality
    * BDD (Behavior Driven Development) is a subset of TDD - describe the behavior, instead of just asserting the final result
  * Integration Tests - put them all together
  * Acceptance Tests - test on devices
  * Stress Tests - load testing

# Development Process

1. Develop locally
    1. `git checkout -b &lt;branch-name>`
    2. Make changes, test then commit and push to remote branch
2. Deploy to Staging
    3. Change STAGING_BRANCH on Travis to point to remote branch
    4. Trigger another build on Travis
    5. Test on Staging
3. Merge from feature branch to master
    6. create PR
    7. Squash and Merge to master
4. Deploy to Production
    8. create release candidate -`git checkout -b release-1.6.1`
    9. create Pull Request for`release-1.6.1 to release`
    10. create Pull Request for `release-1.6.1 to master`
    11. **IMPORTANT**
        1. *deployment happens only when you create **MERGE**
        2. **always use **MERGE **and DON’T SQUASH because we want to make sure git ID matches

# Digital Transformation

* fast discipline better than slow chaos
* Automate whenever possible because bots do certain jobs better than humans
* Digital startups can take down traditional slow moving companies because of their speed

# Software Design

* [https://open.spotify.com/episode/5WDpHXyKrcmB4aALoGr0Ru?si=Wf8koLgPTO6fmZVh9ZFelQ](https://open.spotify.com/episode/5WDpHXyKrcmB4aALoGr0Ru?si=Wf8koLgPTO6fmZVh9ZFelQ)
* Stable guarantee and the assumptions you make about your design - ie using Lambda to pull list of institutions onLoad means that if a new institution is added while Lambda is still running it will not get loaded

# Product Management

* Vision (ideal state of world)
* Use Cases or functionality
* Options
* Narrow down and why
* [Launch] [Good Products]
  * [Launch]
    * Stakeholder Mgmt
    * on time
  * [Good Products]
    * technical
    * design - think through all the possibilities
      * talking to users, start building for 1 user
      * competitive analysis - think more broadly about who your competition is
        * scope, con, why is it designed that way
      * concepts - think about extreme scenarios
    * analysis
    * Efficiency
* Product Strategy
* Marketing Strategy
  * for users, these are the problems that we have found, this is how we have solved it.
  * so that they themselves
  * long term
    * right now forms only handle your
    * bring down to real moments that people will experience
    * how can formSG help you
  * long term strategy is at the end
    * right now we can only handle the basic forms, we want to move towards a state where

# Coding Tech

* Develop Debug Learn - [https://youtu.be/Jmi2bxkOl0I](https://youtu.be/Jmi2bxkOl0I)
  * Use good
* API Security - [https://youtu.be/hoZ3YY-2B2E](https://youtu.be/hoZ3YY-2B2E)
  * 82% of Akamai traffic is for APIs, making API security really important
  * don’t publish API documentations to public, at least make it behind a registration gate - documentation gives hackers lots of info about how to Attack your system
  * pretty scary how banks have weak integration security (eg private keys without password, hard coded API tokens in source code or URL)
  * #3 happens because these apps are often built by outsourced or offshore companies and run by marketing teams who don’t understand security
  * don’t put tokens in URL because it gets logged or is visible in refer
* How Does YouTube Recommend Videos -- AI EXPLAINED - [https://youtu.be/GAm9qoUX1XM](https://youtu.be/GAm9qoUX1XM)
  * Let’s say we have a video site
    * 5 videos and 5 users
    * A user gives +1 if he likes the video, -1 if he dislikes, 0 if hasn’t been watched
    * We want to predict whether User D will like Video 3
  * _Sparsity - the problem of incomplete data because not everyone has watched every video_
  * **Collaborative Filtering - making prediction by collecting lots of data from multiple people**
    * User Based Collaborative Filtering
      * Find how similar users are
        * Normalise takes into consideration different strictness of users - by computing mean of every single user and subtracting that from their ratings. This makes every users’ mean rating = 0
        * Cosine Similarity calculates how similar 2 vectors are - smaller angle means more similar
      * Make a prediction
        * Use weighted average with other users who have given rating to Video 3
        * If value &lt; 0, User D will likely not like Video 3 (since every users’ mean rating = 0)
    * Item Based Collaborative Filtering
      * Why does this perform better than User-User CF?
        * Items are easier to categorise
        * Rate of increase in items &lt; rate of increase in users
    * Pros - Simple to implement
    * Cons - Doesn’t scale well
  * **Matrix Factorization - reduce number of dimensions by comparing Users and Items directly**
    * Pros - Scalability
    * Cons - Interpretability
      * Vectors are transposed to latent space - We may know that they are very similar, but won’t be able to tell why they are similar
  * **Deep Learning**- not all users will rank videos, so we will need other “signals” to derive whether users like something or not
    * Candidate Generation - find a whole bunch of videos that users may like
      * User Context: Watch History, Search History, Location, Device Type, Gender, Age, Video Freshness
      * Use a Neural Network that takes in User Context into a list of videos
    * Ranking - sort them by relevance
      * Example Features
        * What videos were watched
        * How many videos has the user watched?
        * When was the last time a user watched a video on this topic?
      * Ranking is expensive, hence we use Candidate Sampling
      * Relevance Score is calculated based on **Weighted Logistic Regression**
        * Input - Hundreds of video features, user context
        * Output - Relevance Score (Expected Watch Time)
        * The formula maximises the probability of seeing a video that is watched, and minimises odds of watching video not watched
      * As a result, longer videos tend to be shown more than shorter videos because they have higher expected watch time
* Full-Stack Serverless with TypeScript - [https://youtu.be/4fqzPW24cLM](https://youtu.be/4fqzPW24cLM)

# PELP01: Procurement

* [https://www.learn.gov.sg/dlp/student/tagcollection/140](https://www.learn.gov.sg/dlp/student/tagcollection/140)
* Key Principles
    1. Open and Fair competition
    2. Transparency
    3. Value for money
* Lifecycle
    4. Establishing needs (AOR)
    5. Determine Procurement Approach
        *Check for Demand Aggregation contracts
            *   Period Contracts
            *Framework
        *   SVP - &lt; 6k
        *ITQ - 6k - 90k
        *   ITT - > 90k
        *EPVs exclude GST
    6. Specify requirements
        *   Ranked evaluation criteria
    7. Sourcing
        *SVP - Prices must be reasonable, e.g.
            *   Prices are openly available in media
            *Recent quotes
        *   Quotation
            *Open Quotation (default, open to all)
                1. Minimum 7 working days for people to submit quote, and must also close quotation on a working day
            *   Limited Quotation (can just be one or few suppliers)
            *If there are changes to requirements, put up a corrigendum and publish it via the same media that the original quotation was released
            *   Allowable conditions for limited quotation
                2. No open quotes received
                3. Only one supplier can meet the needs
                4. Economic or technical reasons to maintain interoperability with existing infrastructure, or would cause significant inconvenience or substantial duplication of costs
                5. Urgent
                6. Prototyping
                7. In public interest to limit competition
                8. Goods purchased on commodity market
                9. Exceptionally advantageous conditions (e.g. fire sale)
                10. Engaging winner of a design competition (competition is organised according fairly)
            *QAA can still approve outside of above conditions
            *   All reasons must be included in the Quotation Report
        *Tender
            *   ITT
                11. Open Tender (default, open to all)
                12. Limited Tender
                    *No minimum open time
                13. Selective Tender
                    *   2 stage process where suppliers must meet pre-tender qualification before they can submit tender
                14. If there are changes to requirements, put up a corrigendum and publish it via the same media that the original quotation was released
                15. Allowable conditions for limited tender
                    *No open quotes received
                    *   Only one supplier can meet the needs
                    *Economic or technical reasons to maintain interoperability with existing infrastructure, or would cause significant inconvenience or substantial duplication of costs
                    *   Urgent
                    *Prototyping
                    *   In public interest to limit competition
                    *Goods purchased on commodity market
                    *   Exceptionally advantageous conditions (e.g. fire sale)
                    *Engaging winner of a design competition (competition is organised according fairly)
                16. Can still use limited tender if both the below are met
                    *   Not covered under WTO-GPA
                    *Approved by PS/CE
            *   Request for Proposal
                17. Suppliers are free to submit solutions/proposals as long as it meets the requirements of the GPE
                18. Usually Open Invitation, but can be limited RFP
        *Direct Contracting
            *   Opportunity not known publicly and did not go through formal Tender or Quotation procedures
            *With one supplier only
            *   Must meet conditions of limited quotation or tender, and with approval
            *   To adopt all other downstream procedures
* Request for Quotation
  * When existing DA is available, we use RFQ for Framework Agreements

    8. Evaluating
        * Evaluation Committee
            * officers doing evaluation cannot be the same as the approving authority
            * Should also declare whether there are conflict of interests
        * Evaluation criteria must be made known to all suppliers
        * Value For Money does not necessarily mean the lowest cost
        * Can ask for extension if need more time, but tenderers who disagree with the extension will have the tender invalidated after the initial time
        * Check for debarment of tenderers
        * Approving Officer (PS or delegated officer) can allow for amendments of quotation if it’s erroneous
        * Cannot revise bids after ITQ/ITT has closed, but can make changes to requirements by recalling and calling for another
    9. Seeking Approval
        * Approving Authority depends on APV
            * &lt;= $90k - QAA approval
            * &lt;= $1m - Tenders Board A (CEO and 2 members of seniority)
            * 1m - 10m - Tenders Board B (CEO and 2 members of seniority)
            * > $10m - Tenders Board C (Minister and PS and 1 member of seniority)
        * Framework Agreement
            * &lt; $1m - QAA
            * &lt; $10m - Tenders Board A
            * > $10m - Tenders Board B
        * Period Contract
            * No Limit - AO AOR
        * Always make sure no conflict of interest
    10. Contracting
        * Acceptance of Quotation
            * Must execute acceptance of quotation or tender proposal through writing, contracts or purchase order
            * Award Notice should be published in GeBIZ no later than 3 days
        * Handling unsuccessful tenderers
            * Explain
                19. Why proposal not selected
                20. Characteristics of winning tenderer
                21. Name of winning tenderer
            * Can withhold information for legal reasons, fair competition, intellectual property rights
    11. Managing Contracts
        * Contract Administration
            * Goods or Service Receipt
                22. Use documents such as delivery order, inventory report, vendor log book or maintenance log book for intangible services
                23. Should not be payment certifying officer or approving officer
            * Payment Certifying and Approving officer should check that
                24. Proper approvals have been obtained
                25. Procurement procedures have been complied with
                26. Services are satisfactory
                27. Invoice amount is correct
        * Managing contracts and suppliers
        * Contract Variation
            * Especially when APV is increased
            * Always include past approved contract variations - esp important to look at the cumulative amount
            * Prices for changes in scope may no longer be competitive since it’s not open, therefore consider add-on in initial contract
        * Debarment of contractors
* Debarment period should commensurate with financial or material losses suffered by the GPE
* Can also issue warning letter instead
* Mindset and Ethics

# CS50 for Lawyers

[link](https://cs50.harvard.edu/law/2019/)

* Programming Languages
  * Compilers
  * Interpreters
  * Virtual Machines
* Data Structures and Algorithms
  * Performance Calculation
    * Big O notation - maximum time - below shows ranking from best to worst
      * O(1)
      * O(log n)
      * O(n)
      * O(n log n)
      * O(n^c)
      * O(c^n)
      * O(n!)
    * Omega notation - minimum time
    * Theta notation - max and min is the same
  * Searching
    * Binary search gives O(log n)
  * Sorting
    * Bubble sort
    * Selection sort
    * Merging sort
      * O(n log n)
      * Ohm(n)
      * Faster, but also takes up extra memory for temporary storage
  * Data Structures

<table>
  <tr>
   <td>
   </td>
   <td>
Array
   </td>
   <td>Linked List
   </td>
   <td>Binary Tree
   </td>
   <td>Hash Table
   </td>
  </tr>
  <tr>
   <td>Index
   </td>
   <td>O(1)
   </td>
   <td>O(n)
   </td>
   <td>O(log n)
   </td>
   <td>O(1)
   </td>
  </tr>
  <tr>
   <td>Search
   </td>
   <td>O(n)
   </td>
   <td>O(n)
   </td>
   <td>O(log n)
   </td>
   <td>O(log 1)
   </td>
  </tr>
  <tr>
   <td>Sort
   </td>
   <td>O(n)
   </td>
   <td>O(n)
   </td>
   <td>O(log n)
   </td>
   <td>O(log n)
   </td>
  </tr>
  <tr>
   <td>Insert
   </td>
   <td>O(n)
   </td>
   <td>O(1)
<ul>

<li>Append O(1)

<li>Prepend O(1)
</li>
</ul>
   </td>
   <td>O(log n)
   </td>
   <td>O(1)
   </td>
  </tr>
  <tr>
   <td>Pros
   </td>
   <td>Efficient for sorting and searching because elements are back-to-back-to-back
   </td>
   <td>Easy to add new elements at the end since we just store address of next element
<p>
<strong>Implements stacks and queues</strong>
   </td>
   <td>Easy to add and relatively faster to sort and search
   </td>
   <td>combination of Arrays and Linked Lists
   </td>
  </tr>
  <tr>
   <td>Con
   </td>
   <td>Expensive to add new elements because they will have to move the entire chunk in memory
   </td>
   <td>Takes up more memory since we have to store address in addition to value
   </td>
   <td>Depending on what values get added, may need occasional rebalancing of tree to maintain performance
   </td>
   <td>
   </td>
  </tr>
</table>

* Cryptography
  * Art and science of protecting information against potential attacks
  * Cipher
    * Reversible
    * Algorithms used to obscure (encipher) or reveal (decipher) information
    * Substitution Cipher
      * Attack Vector: key is prevalent, so anyone who has access will be able to crack the cipher
      * Types
        * Rotational (Caesar) Cipher
          * Substitution Cipher, but wrap the values around
          * Limited by number of keys (only 26)
        * Vigenere Cipher
          * Using a keyword, sum the letters together and show the final letter
          * E.g. HELLO with LAW gives TFIXP
          * Pros - the same letter of plain text does not give the same encrypted letter
          * Number of keys - 26^n
      * Can still be cracked with Frequency Analysis because letters appears in a somewhat similar pattern
  * Hashes
    * Irreversible
    * Good hash
      * Use only the data being hashed
      * Use all of the data being hashed
      * Be deterministic (same input gives same output)
      * Uniformly distribute data
      * Generate very different hash codes for very similar data (e.g. LAW and LAWS should look very different)
    * Very unlikely to have collisions (will never be guaranteed)
  * Modern Cryptography
    * Relies on variations of hashing
    * Good hash functions
      * Computationally impossible to reverse
      * Be deterministic
      * Generate very different hash codes for very similar data (e.g. LAW and LAWS should look very different)
      * Never allow two different sets of hash to return the same digest
    * SHA-1
      * Digest is always 160 bits
    * SHA-2, SHA-3
    * MD5, MD6
    * Uses
      * Email
      * Secure web browsing
      * VPN
      * Document storage
    * Public Key Cryptography
      * Two hash functions, one reverses the other
    * Digital Signatures
      * Opposite of encryption
      * Verify the authenticity of the sender of the document
      * 2^256 bits
      * Blockchain
        * A bit like a linked-list, each “node” has 4 pieces of data
          * Previous node pointer
          * Next node pointer
          * Data (ledger of transactions digitally signed)
          * Proof of work - consensus of the blockchain users that this is the correct one
        * Because it is decentralised, when a dispute happens, the node with the largest proof of work is the correct one
        * A miner finds a key that generates 30 consecutive zero bits at a start
          * Probability is 1/2^30
        * A transaction is a contract on blockchain
        * And can be any data (like a PDF) - which is what Ethereum uses
  * Cybersecurity
    * Memory
      * Items have to be moved to RAM before it can be processed
      * 32 bit vs 64 bit
        * 32 bit can process memory addresses up to 32 bits in length (memory address 000000… to 32,000,000,000)
        * Can extend using virtual
      * Memory requires power, and with no power, electrical charge dissipates and state is lost
      * 2.6 GHz - means can do 2.6 billion 4-byte operations per second (if on a 32 bit)
      * Cost
        * CPU Memory
        * L1,2,3 Cache
        * RAM
      * Hard-disk space (not solid state)
        * (solid state drive vs hard disk drive) - SSD is more secure
        * Does not use power, but use magnets to determine 1 or 0s.
        * Ways that hard drives fail
          * read/write arm has jammed
          * Hard disk arm breaks
        * When deleting a machine, it just “forgets where the file lives”, even if it's the Recycle Bin
    * Digital Forensics
      * A forensic image that replicates the content of the file “bit-by-bit”
      * The first few bytes of the file denotes what file type this is
      * How to ensure that files are actually deleted
        * Shredding the hard drive
        * Degausser (magnet)
        * Secure Empty Trash (overwrites the data with random bits)
          * Not good enough because it only makes a single pass, and there will be a remaining halo effect
          * The industry standard is to make 7 passes
      * Strategies to protect data
        * Encrypt your hard drive (so that password must be entered to “open up the hard disk”)
        * Avoid insecure wireless networks (traffic can then be sniffed)
        * Use VPN
        * Password Managers (avoid using the same passwords)
          * Password Strength
            * 8 characters can be brute forced in a few days
        * Backing up data
                    *Useful to fight against ransomware
                    *   Backup to offline way - non-network computers, flash drives etc
        * Have an archival plan - e.g. remove after 5 years
        * Make data security a priority
        * Establish compliance protocols
    * Git
      * Protecting against accidental password commits
        * `git-secrets` : uses a regex to warn if code potentially contains passwords
        * Limit 3rd party tools
        * Use commit hooks to check for passwords
        * Use SSH key
        * Use `git rebase`to remove and change history
        * Mandate use of 2FA
    * DDoS - distributed onto multiple machines
      * DoS - just a single machine
      * Botnet
        * Distribute worms or viruses into machines, then activates it to do DDoS
      * Collateral damage when server is hosted on cloud, 1 company being DDoS attacked may affect other businesses on the same physical hardware
      * Ways to avert DDoS
        * Firewalls - helps to protect against DDoS by limiting traffic only on certain ports
        * Sinkholing - throw away all the traffic that comes in
        * Packet Analysis - identify suspicious traffic and block those
    * HTTPS
      * It’s more secure than HTTP because packets jump through multiple routers in between that can sniff your traffic
      * SSL/TLS Cert
        * Certificate Authority - as a whole we trust that the CA can verify that public key is indeed mine
        * How it works
          * Client browser checks CA for server public key, then uses it to send an initial request
          * Server decrypts using private key. Server responds with a new key encrypted with client public key.
          * The new key is a session key (AES cipher - which is reversible) that is used to encrypt/decrypt all messages in the session (until user closes the browser)
          * The reason we use a cipher instead of public/private key is because of performance. Ciphers can be mathematically reversed much faster
    * Cross Site Scripting (XSS)
      * XSS vulnerabilities exist when an adversary tricks the client’s browser into running local code
      * How to protect against
        * Sanitise inputs - such as replacing `&lt;>`with `&lt;` and `&gt;`
        * Disabling javascript
        * Disabling inline javascript
        * Content Security policy - add to HTTP header
    * Cross Site Request Forgery (CSRF)
      * Exploiting a cookie (when user is authenticated) to make an outbound request you didnt want to make
      * E.g. transferring of funds by clicking a link
      * How to protect against
        * Don’t use GET requests for state changing operations
        * Use SameSite Cookie attribute - when set to Strict, cookies are not sent with cross-site requests
        * Implement UX defense such as OTP, Captcha
    * Databases
      * Hash passwords can still be hacked because it’s deterministic.
      * And most common password is “password”
      * SQL injection - DROP TABLE or WHERE (password = ‘1’ OR ‘1’ = ‘1’)
        * Simple way to guard against latter is to escape by replacing single quotes with double quotes
        * E.g. `WHERE password = '1" OR "1" = "1'`which will now be okay
    * Phishing
      * Simple way is to do `&lt;a href="url1">url2&lt;/a>`.
  * Internet Technologies, Cloud Computing
    * DHCP - assigns IP address, and says where the next hop is
    * Default Gateway - For packets that we want to send outside of our private network, it will be sent to the default gateway (router) to hand in further down.
      * Its purpose is to change the private IP address, to the public IP address using a Network Address Translator (NAT)
    * IP
      * Sender and recipient address
      * Fragmentation
    * TCP
      * Guarantees delivery
      * Uses source and destination port
    * DNS
      * Domain name server translates domain names to IP addresses
  * Web Development
  * Database Design
    * CHAR(2) forces 2 characters all the time
    * VARCHAR(20) allows a maximum of 20 characters, but can be shorter depending on the value
    * As a result, CHAR(2) is actually more efficient because the computer can jump to the exact memory quickly at O(n), as compared to VARCHAR(2) which requires linear search
    * Race Conditions
      * When 2 updates happen together at the same time
      * Solved with table locks
    * Deadlocks
      * Solutions
        * Prevention - Preventing it altogether
        * Detection - know when it happens then rollback
        * Ignorance - let it happen then reboot
    * SQL injection
      * Escape works by adding a forward slash in front of such keys. So `SELECT * FROM artist WHERE title='haha';DELETE;'` becomes `SELECT * FROM artist WHERE title='haha'\;DELETE'` and automatically becomes part of the query string instead
    * Scalability
      * Using read replicas
  * Trust Model
    * GPL license (copyleft)
      * Any code that uses GPL code then also needs to be open-sourced
    * Limited GPL
      * Limit only to changes you have done on the library using LGPL
    * MIT
      * Do whatever you want
  * AI/ML
    * Artificial Intelligence - pattern recognition, e.g. document review
      * Humans supply data and rules
      * Neurogenetic - provide target and AI generates algorithms to get itself there
    * Machine Learning
      * Neurogenetic to arrive at Shakespeare’s “a rose by any other name”
        * init - randomly generate strings with 23 characters
        * update_fitness - determine whether it is correct or not by
          * seeing if the right character is in the right spot
        * Crossover - merge best traits from “mother” and “father” to potentially form a better child by
          * take two strings and match them together to potentially form a better string
        * Mutate - change a bit of the child so that we don’t potentially end up with everything bad
          * randomly change one of the characters in the child string
        * Pseudocode
    * Net Neutrality

# System Design

* 4 steps
    1. Use Cases and Constraints
    2. Abstract Design
    3. Understanding bottlenecks
    4. Scaling the abstract design
* Use Cases and Constraints
    5. Use Cases - come up with a few and narrow down
    6. Constraints - traffic and data
        *How many requests/month - then narrow it down to requests/seconds
        *   How much data per request - then calculate the required
* Abstract Design
    7. UI layer
    8. Application service layer
    9. Data storage layer
    10. Caching (if any)
* Understanding bottlenecks
    11. Will traffic or data be a problem?
    12. Need load balancers?
    13. Will the database be too slow, need to replicate etc?
* Scaling
    14. Vertical scaling
    15. Horizontal scaling
    16. Load balancing
    17. Database replication
    18. Database partitioning

# Advanced Product Management (Udemy)

## Vision, Strategy, Metrics

[https://learncsc.udemy.com/course/advanced-product-management-vision-strategy-metrics/](https://learncsc.udemy.com/course/advanced-product-management-vision-strategy-metrics/)

* **Global Vision -**educated guess of what the world is like in the future
* **Company / Product Vision**- where the company / product is going to fit in the global vision
* **Strategy**- what action you take, to increase your chances of success
  * Competition Strategies
    * Cost
    * Differentiation
    * Focus
      * Cost
      * Differentiation (e.g. Instagram who focus on photos using filters)
  * Happens at all levels, and no other way than to know your market, customers and technology better
* **Roadmapping**
  * Nearly always inaccurate when you are doing agile
  * Roadmap is useless without a clear global vision, product vision and goals
* **Metrics**
  * How to pick good metrics
    * Exploratory metrics vs Reporting metrics
      * Exploratory is short term (e.g. how often is someone clicking on a button) and help us to make informed decisions
      * Reporting is long term (to make sure your product is getting better over time)
    * Reporting Metrics should be rate or ratio
  * Lagging vs Leading Metrics
        *Lagging - changed as a result of other metrics (e.g. weight)
        *   Leading - changes other metrics (e.g. calories consumed/burnt)
        *   A metric can be both lagging and leading at the same time
  * How to design Cohort Analysis
    * 3 Anchors
      * Time - e.g. 1st - 7th Aug
      * Lagging period - 1 month
      * Termination date - 7th Sep
  * What could go wrong with metrics
    * When you can’t justify huge changes, always **sort by origin source** (e.g. google ads, facebook ads, organic etc)
  * T-test
    * helps to deal with problems of averaging
      * Are cohort values meaningfully different?
      * Do we need to wait to get more data?
    * Variance
      * Higher variance means lower accuracy of average because the difference between values are very high
    * If T-value is high, difference between cohorts is meaningful. If T-value is low, then it means it’s more likely due to chance
    * Value is usually between 0-2.5. Above 1 means something is going wrong
    * T-tests are meant to be done on sample size &lt;150 pax, if you want to run on entire population you should use a Z-test
    * Formula
      * x: mean, s: standard deviation, n: sample size
      * Numerator: difference between the average of both numbers
      * Denominator:
        * Variance = Square of standard deviation
    * After calculating the T-value, refer to a T-table to determine what T-value should be based on sample size and degree of certainty we want
    * Degrees of freedom - Sum of both sample size minus 2
      * ((n1 + n2) - 2)
  * Intuitive vs. Data
    * Data is better for optimising existing funnels and making incremental changes than for large strategic changes
    * Not so good for getting approval of a new product
    * For large strategic change, more likely have to take the chance
  * E-commerce metrics
    * Average Order Volume - size of each checkout
      * Note that this is different from CLTV, which is a more long-term revenue metric.
      * AOV is more immediate term - e.g. new startup, or campaign success
      * Still good to segment by origin source
    * Conversion rate (by origin source)
  * Mobile App Metrics
    * AARRR
    * Engagement rate
      * Sessions per DAU - for every active user each day, how often do they launch the app
      * CTR on push notifications, email
    * Retention
      * N day Retention: on any given day, what percentage of the total users launch the app
      * Churn and App Uninstalls
        * Your own definition of churn
    * Acquisition
      * Download attribution
      * CPI
    * Activation metric
      * % of downloads that launch the app
      * Generally, 80-85% activation rate
    * Revenue metrics
      * Free
        * Will more likely track usage metrics
      * Freemium
        * % of upgrade users
        * % of upgrade by acquisition source
        * Purchases per month
      * paid apps
        * How many people pay for downloads
        * More likely playing with price points
      * ARPU
      * CAC
      * CLTV
  * Marketplace metrics - mostly similar to AARRR, but below highlights the difference
    * Revenue
      * GMV
        * If it’s service related, then will further breakdown into
        * Contracted GMV
        * Delivery GMV
      * Take Rate
      * AOV
      * Contribution margin = total value of take rate - variable costs
    * User Activity
      * Liquidity - how much of each others’ products or services are each other buying
        * % of items / items sold within a period of time
        * Provider Liquidity
          * Frequency of which a listing creates a sale or transaction for the listing owner
        * Customer Liquidity
          * Conversion Rate - Odds of any given user buying something when they come to a page
      * Cohort consistency
      * Fragmentation
        * High - a lot of users doing a little - likely mean the marketplace is more likely to stay useful
        * Low - little users doing a lot
          * E.g. if amazon only had 5 sellers
            * A lot of power over the platform
            * Can easily discourage other sellers from trying to join
            * Upward price pressure on goods
            * Marketplace would lose its competitive edge
        * Whale curves
    * Customer Satisfaction
      * NPS, Product reviews, Refund rates
      * Order fulfilment - % of orders fulfilled, time to fulfillment

## Leadership & Communication

[https://learncsc.udemy.com/course/advanced-product-management-2-leadership-communication](https://learncsc.udemy.com/course/advanced-product-management-2-leadership-communication)

* Presentations
  * Cast your hook
    * “I’m going to show you how to…”
    * Give a credible statement
  * Engagement
  * Practice
  * Audience
    * In person (big group)
    * Informational deck (sent informally over email)
  * Visuals
    * Never use 100% black for text on white background
    * Color palette - only one or two primary colors. Can find complementary colors on colors.adobe.com
  * Can find images from [https://unsplash.com/](https://unsplash.com/)
* Storytelling
  * Tell a story for emotional connection
    * Style 1
      * Ideal future
      * Present day issues
      * How the product solves all the issues (as the superhero of the story
    * Style 2
      * Current state of affairs (suboptimal)
      * Leap into the future where the problems don’t exist. Lay out plan, product idea w
      * Make connection to the present - data points
    * Passion
* Public Speaking
  * Get organised, prepare and practice
  * Speak with excitement
  * Focus on the material rather than the audience
  * Focus on the way you say the words (volume, emphasis etc), lesser than the vocabulary etc
  * Have approachable demeanor
* Body language
  * Maintain neutral position, feet shoulder width apart, hands by your side.
  * Gestures
    * Positive gestures - hands facing outwards show openness, Put hands on chest to represent sincerity, chopping motion when driving a point
    * Negative gestures - cross arms, pointing (too domineering)
  * Facial expressions
    * Keeping the other person’s gaze
  * As a listener
    * Lean forward slightly
    * Maintain eye gaze
    * Keep hands at sides
    * Use facial expression to show listening
* Personality Types
  * Traits
    * The Big 5
      * Openness (curious vs cautious)
      * Conscientiousness (organised vs careless)
      * Extraversion (outgoing vs solitary)
      * Agreeableness (friendly vs challenging)
      * Neuroticism (nervous vs confident)
    * Most useful when you know the traits of who you are talking to
  * Good documentation
    * Examples - Email updates, Meeting notes, PRD, software tickets, blog posts, wiki or knowledgebase posts, post mortem notes
    * Benefits
      * Understanding and time saving
      * Easily look back - explain why you did what you did
      * Saves time onboarding
      * Makes you look really good
    * How to do it
      * Record everything
      * Leave no questions unanswered (what, why, when, thoughts, results, list unanswered questions explicitly)
      * Establish regular documentation schedule
      * Organise it
* Leadership
  * Becoming a leader
    * Understand yourself (limits, strengths, needs), flexible (reflect on past, learn from mistakes)
    * Motivate your teams (respect opinions, trust, treat people fairly)
    * Be creative (open to ideas)
    * Act like a role model
    * Stay connected to emotions
    * Act with humility (real, reasonable, accountable)
    * Show passion for what you do
    * Communicate (and listen)
  * Communication
    * Ask for input
    * Request feedback
    * Encourage reflection
    * Provide feedback
    * Keep criticism constructive (offer alternative behaviours)
    * Never give criticism publicly (some people prefer compliments in private too because they dont want to be the centre of attraction)
    * Quickly address any misconceptions
  * Influencing without authority
    * Build reputation as expert
    * Be an effective problem solver (try solving it yourself before asking others)
    * Give credit to team where credit is due
    * Empathetic, positive attitude
    * Show passion for career (share compelling stories)
    * Appeal to emotion (story telling)
  * How to make yourself visible
    * Never eat lunch alone
    * Make presentations
    * Use social media
    * Jump in with both feet
    * Request professional development (then share with others what you learn)
* Managing Upwards
  * Make it easy to manage you
  * Help them out whenever you can
  * Know when to push back or ask for something
  * How to say no
    * People agree with the hypothetical idea of focusing (and not doing it), but tend to fail actually practicing it
    * “If you haven’t gone through a whole lot of hard decisions to focus, you haven’t actually focused”

*
