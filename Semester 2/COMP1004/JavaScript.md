> Quiz is likely to be on the first wee


JavaScript is a scripting language that allows the implementation of dynamic content on web pages.

It has almost achieved feature parity with other languages such as OOP classes, static typing and more.

### APIs
APIs are ready-made sets of functions to implement new programs.

There are 2 categories of APIs:

#### Browser APIs
Browser APIs - built into the web browser.
	- The DOM (document object model) API allows us to manipulate HTML and CSS
	- Geolocation API to get geographical information
	- Canvas, WebGL and WebGPU APIs allows us to create (animated) 2D and 3D graphics.
#### Third-party APIs
Third-party APIs are those not built-in to the browser
	- Google Maps/OpenStreetMaps to embed custom maps into the website
	- Twitter API - display own tweets on own website

In HTML
There are two ways to add JS:

**Internal**
```html
<script>
	// JS here
</script>
```

**External**
```html
<script src=“script.js” defer></script>
```
`defer` is preferred as it will download in parallel and, after the parsing of the HTML, run the script.

**Inline**
```html
<button onclick=“doSomething()”>Click me!</button>
```

## Syntax
### Variables
`let` is preferred over `var` (some scope changes but generally the same)

- Variables must not start with underscores (only in special constructs) or numbers. 
- camelCase is preferred.
- Variables are case sensitive

#### Constant
Used with the `const` keyword. They cannot be assigned with another value after initialisation.

A constant can be defined as an object, with attributes that can be changed.

```js
const bird = { species: “kestrel” };
bird.species = “kingfisher”; // this is completely fine!
```

#### Strings
Single quotes, double quotes or backticks can be used to wrap strings in.

Backticks can include a dollar sign and curly brackets to subsitute in another variable. These are known as *template literals*.

```js
let name = “John”;
var string = ‘Hello, ‘;
console.log(`${string} ${name}!`)
```

We can also have properties (and functions) on strings

- Properties can be accessed by the . operator

`string.length;` returns an int of the string’s length.

Funcitons include indexOf, slice, and replace

```js
const string = “MDN - resources for developers by developers”
console.log(string.indexOf(“developers”))’ // returns 20

// print the range between 1 (incl) and 4 (excl)
let newString = “mozilla”;
console.log(newString.slice(1, 4)); // ”ozi”

console.log(newString.replace(“moz”, “van”)) // ”vanilla”
```


### Arrays

Changing items & 2d arrays
```js
const shopping_list = [“bread”, ”cheese”, “milk”, [0, 1, 2]];
shopping_list[0] = ”pasta”;

shopping_list[3][2]; // = 2
```

We can also use `indexOf()` on arrays to get the index of that item.

- To add elements to the end of an array we can use `object.push()`
- To add elements to the start of the array we can use `object.unshift()`.
- To remove the last item, we can use `object.pop()` - which also returns the removed value
- To remove the first item, use `object.shift()`
- To remove a specific item at an index, use `object.splice(index, 1)`
- A string can be converted to an array with `object.split()`



Ternary operator

This is shorthand for if/else statements
```js
condition ? yes_code : no_code 
```


### Iteration
```js
const cats = ["Leopard", "Serval", "Jaguar", "Tiger", "Caracal", "Lion"];

// 1. traditional java-y wy
for (let i = 0; i < cats.length; i++) {
	console.log(cats[i]);
}

// 2. javascripty way
for (const cat of cats) {
	console.log(cat);
}
```




### Functions




#### Anonymous functions

```js
(function () {
	alert(“Hello”);
})
```
Useful for when a function is passed as a parameter

```js

// Traditional implementation
function logKey(event) {
	console.log(`You pressed "${event.key}".`);
}

textBox.addEventListener(“keydown”, logKey);

// Anonymous
textBox.addEventListener("keydown", function (event) {
	console.log(`You pressed "${event.key}".`);
});
```


Arrow functions
A way to pass anonymous functions without writing as much code.

```js
// Arrow
textBox.addEventListener("keydown", event => {
	console.log(`You pressed "${event.key}".`);
});
```



