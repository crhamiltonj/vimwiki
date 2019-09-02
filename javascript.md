# Javascript

<img src="https://upload.wikimedia.org/wikipedia/commons/6/6a/JavaScript-logo.png" width=100px>

## What is it

- Javascript is a lightweight, cross-platform, object-oriented computer programming language.
- JavaScript is one of the three core technologies of web development (the other two are HTML and CSS)
- Today Javascript can be used in different places:
  - Client-Side: Javascript was traditionally only used in the browser
  - Server-Side: With node.js we can use JavaScript on the server too
- Javascript is what makes modern web development possible:
  - Dynamic effects and interactivity
  - Modern web applications thatn we can interact with
- Frameworks like React and Angular are 100% based on JavaScript: you need to master JavaScript in order to use them!

---

## Comments

### Single Line and Multiline

- JavaScript comments
  - Single line comments are `//`
  - Multiline comments are `/* */`

---

## Variables

A container to store a value that you can use over and over

### To declare a variable

```javascript
var firstName = "John";
```

- Use the var keyword to tell javascript that you are creating a variable
- the item on the left side is the name of the variable
- the item on the right side is the value the variable contains

### Datatypes

- Number: Floating point numbers for decimals and integers
- String: Sequence of characters, used for text
- Boolean: Logical data type that can only be `true` or `false`
- Undefined: Data type of a variable that does not have a value yet
- Null: Also means 'non-existant`

Javascript has dynamic typing: data types are automatically assigned to variables

### Variable Names

- Variable names should be descriptive
- Javascript convention is to use camelCase variable names
  - the first letter is lowercase
  - each following word the first letter is uppercase

#### Rules

- Variables cannot start or contain characters with numbers or symbols that are not \\\\\\\\\\_ or \$
- Reserved JavaScript keywords cannot be used as variable names

### Variable Mutation and Type Coercion

- Type Coercion -- JavaScript automatically converts certain variables so that the can be combined with other variables of another type.
- Variable Mutation -- JavaScript will also convert the type of a variable upon reassignment with a different type.

---

## Operators

### Basic Operators

#### Mathematical

- `+` Addition
- `-` Subtraction
- `*` Multiplication
- `/` - Division

#### Logical

- `<` - Less Than
- `<=` - Less Than or Equal To
- `>` - Greater Than
- `>=` - Greater Than or Equal To

#### typeof operator

- `typeof` - Return the type of a variable

#### Assignment

- `=` - Assign value on the right to variable on the left
- `+=` - Add value on right to item on left and assign result to left
- `-=` - Subtract "
- `*=` - Multiply "
- `/=` - Divide "

#### Increment / Decrement

- `++` - Increment variable by one
- `--` - Decrement variable by one

### Operator Precedence

If values don't appear to be calculating correcttly check the operator precedence table for precendence and associativity
[MDN Operator Precedence](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Operator_Precedence#Table)

---

## Conditionals and Flow Control

### if / else Statements

if / else statements evaluate a test within parentheses and runs the code within a block if the value is true. If the value is false and an else clause is available it will run the code within the else block.

else and if can be combined to run additional tests.

```javascript
var firstName = "John";
var civilStatus = "married";

if (civilStatus === "married") {
  console.log(firstname + " is married.");
} else {
  console.log(firstName + " is not married.");
}
```

### Boolean Logic

- `&&` - Logical AND - Returns `true` if both sides of expression are true
  and `false` if either side is false
- `||` - Logical OR - Return true if left side is true
- `!` - Logical NOT - Invert the true or false value

### Ternary Operator

Evaluates a test condition and returns a value base on whether the test is true or false

```javascript
var firstName = "John";
var age = 16;

age >= 18
  ? console.log(firstName + " drinks beer")
  : console.log(firstName + " drinks juice.");
```

### Switch Statements

```javascript
var job = "teacher";
switch (job) {
  case "teacher":
  case "instructor":
    console.log(firstName + " teaches kids how to code");
    break;
  case "driver":
    console.log(firstName + " drives an Uber in Lisbon");
    break;
  case "designer":
    console.log(firstName + " designs beautiful websites");
    break;
  default:
    console.log(firstName + " does something else");
}
```

### Truthy and Falsy Values

- falsy values evaluate to false in an expression

  - `undefined`
  - `null`
  - `0`
  - `''` (empty string)
  - `NaN` (Not a Number)

- truthy values evaluate to true in an expression: **_any value that is not falsy_**

### Equality Operators

- `==` Equality check with type coercion
- `===` Equality check with strict type checking

## Functions

### Defining and calling functions

Functions are reusable blocks of code that can optionally receive data as input and optionally return data as output.

```javascript
// Defining a function

function calculateAge(birthYear) {
  return 2018 - birthYear;
}

// Calling a function

var ageJohn = calculateAge(1990);
console.log(ageJohn);
```

---

## Function Expressions

### Defining

```javascript
var whatDoYouDo = function(job, firstName) {
  switch (job) {
    case "teacher":
      return firstName + " teaches kids how to code";
    case "driver":
      return firstName + "drives an Uber is Lisbon";
    case "designer":
      return firstName + " designs beautiful websites";
    default:
      return firstName + " does something else";
  }
};

console.log(whatDoYouDo("teacher", "John"));
```

---

## Arrays

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

---

## Objects and Methods

### Object Literals

```javascript
var john = {
  firstName: "John",
  lastName: "Smith",
  birthYear: 1990,
  family: ["Jane", "Mark", "Bob", "Emily"],
  job: 'teacher',
  isMarried: false
};

console.log(john);
console.log(john.firstName);
console.log(john['lastName']);

var x = 'birthYear';
console.log(john[x]);

john.job = 'designer';
john['isMarried'] = true;
console.log john

var jane = new Object();
jane.name = 'Jane';
jane.birthYear = 1969;
jane['lastName'] = 'Smith';
console.log(jane)
```

### Object Methods

```javascript
var john = {
  firstName: "John",
  lastName: "Smith",
  birthYear: 1990,
  family: ["Jane", "Mark", "Bob", "Emily"],
  job: "teacher",
  isMarried: false,
  calcAge: function(birthYear) {
    return 2018 - birthYear;
  }
};

console.log(john.calcAge(1990));
```

#### Accessing members of an Object

```javascript
var john = {
  firstName: "John",
  lastName: "Smith",
  birthYear: 1990,
  family: ["Jane", "Mark", "Bob", "Emily"],
  job: "teacher",
  isMarried: false,
  calcAge: function() {
    this.age = 2018 - this.birthYear;
  }
};

john.calcAge();
console.log(john);
```

---

## Loops and Iteration

[Back to Index](index.md)
