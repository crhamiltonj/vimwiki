# Arrays

```javascript
// Initialize new array
var names = ["John", "Mark", "Jane"];
var years = new Array(1990, 1968, 1948);

console.log(names[0]);
console.log(names.length);

// Mutate array data
names[1] = "Ben";
names[names.length] = "Mary";
console.log(names);

// Array methods

// push add an element to the end of the array
names.push("Sam");

// unshift adds an item to the beginning of the array
names.unshift("Betty");

// pop removes an item from the end of an array
names.pop();

// shift removes an item from the beginning of an array
names.shift();

// indexOf will return the index of the first item that matches the argument
// if indexOf returns -1 the item is not in the array
names.indexOf("Mark");
```

[Back](javascript.md)
