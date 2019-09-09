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

- Variables cannot start or contain characters with numbers or symbols that are not \\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\_ or \$
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

### Function Expressions

#### Defining

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

### for Loops

```javascript
for (i = 0; i < 10; i++) {
  console.log(i);
}

// i = 0, 0 < 10 true, log i to console, add 1 to i
// i = 1, 1 < 10 true, log i to console, add 1 to i
// ...
// i = 9, 9 < 10 true, log i to console, add 1 to i
// i = 10, 10 < 10 false, exit loop

var john = ["John", "Smith", 1990, "designer", false];

for (i = 0; i < john.length; i++) {
  console.log(john[i]);
}

// i=0, 0 < john.length true, log john[0] to console, add 1 to i
// i=1, 1 < john.length true, log john[1] to console, add 1 to i
// ...
// i=4, 4 < john.length true, log john[4] to console, add 1 to i
// i=5, 5 < john.length false, exit the loop
```

### while Loops

```javascript
var i = 0;
while (i < john.length) {
  console.log(john[i]);
}
```

### continue and break Statements

#### continue

```javascript
var john = ["John", "Smith", 1990, "designer", false];

for (i = 0; i < john.length; i++) {
  if (typeof (john[i] !== "string")) continue;
  console.log(john[i]);
}
```

#### break

```javascript
var john = ["John", "Smith", 1990, "designer", false];

for (i = 0; i < john.length; i++) {
  if (typeof (john[i] !== "string")) break;
  console.log(john[i]);
}
```

#### Looping Backwards

```javascript
for (var i = john.length - 1; i >= 0; i--) {
  console.log(john[i]);
}
```

## Functions and Objects

### Function Constructor

```javascript
var john = {
  name: "John",
  yearOfBirth: 1990,
  job: "teacher"
};

var Person = function(name, yearOfBirth, job) {
  this.name = name;
  this.yearOfBirth = yearOfBirth;
  this.job = job;
};

Person.prototype.calculateAge = function() {
  console.log(2019 - this.yearOfBirth);
};

Person.prototype.lastName = "Smith";

var john = new Person("John", 1990, "teacher");
var jane = new Person("Jane", 1969, "designer");
var mark = new Person("Mark", 1948, "retired");

john.calculateAge();
jane.calculateAge();
mark.calculateAge();

console.log(john.lastName);
console.log(jane.lastName);
console.log(mark.lastName);
```

### Object.create

```javascript
var personProto = {
  calculateAge: function() {
    console.log(2019 - this.yearOfBirth);
  }
};

var john = Object.create(personProto);

john.name = "John";
john.yearOfBirth = 1990;
john.job = "teacher";

var jane = Object.create(personProto, {
  name: { value: "Jane" },
  yearOfBirth: { value: 1990 },
  job: { value: "designer" }
});
```

### Primitives vs Objects

#### Primitives

```javascript
var a = 23;
var b = a;
a = 46;

console.log(a);
console.log(b);
```

#### Objects

```javascript
var obj1 = {
  name: "John",
  age: 26
};

var obj2 = obj1;

obj1.age = 30;
console.log(obj1);
console.log(obj2);
```

#### Using Objects with functions

```javascript
var age = 27;
var obj = {
  name: "Jonas",
  city: "Lisbon"
};

function change(a, b) {
  a = 30;
  b.city = "San Francisco";
}

change(age, obj);
console.log(age);
console.log(obj.city);
```

#### Passing functions as arguments

```javascript
var years = [1990, 1965, 1937, 2005, 1998];

function arrayCalc(arr, fn) {
  var arrRes = [];

  for (var i = 0; i < arr.length; i++) {
    arrRes.push(fn(arr[i]));
  }

  return arrRes;
}

function calculateAge(el) {
  return 2019 - el;
}

function isFullAge(el) {
  return el >= 18;
}

function maxHeartRate(el) {
  if (el >= 18 && el <= 81) {
    return Math.round(206.9 - 0.67 * el);
  } else {
    return -1;
  }
}

var ages = arrayCalc(years, calculateAge);
var fullAges = arrayCalc(ages, isFullAge);
var maxHeartRates = arrayCalc(ages, maxHeartRate);
console.log(ages);
console.log(fullAges);
console.log(maxHeartRates);
```

#### Functions returning functions

```javascript
function interviewQuestion(job) {
  if (job === "designer") {
    return function(name) {
      console.log(name + ", can you explain what UX design is?");
    };
  } else if (job === "teacher") {
    return function(name) {
      console.log(name + ", What subject do you teach?");
    };
  } else {
    return function(name) {
      console.log("Hello, " + name + ", What do you do?");
    };
  }
}

var teacherQuestion = interviewQuestion("teacher");
var designerQuestion = interviewQuestion("designer");
teacherQuestion("John");
designerQuestion("John");
interviewQuestion()("Mark");
```

#### Immediately Invoked Function Expressions

```javascript
function game() {
  var score = Math.random() * 10;
  console.log(score >= 5);
}

game();

(function() {
  var score = Math.random() * 10;
  console.log(score >= 5);
})();

(function(goodLuck) {
  var score = Math.random() * 10;
  console.log(score >= 5 - goodLuck);
})(5);
```

#### Closures

```javascript
function retirement(retirermentAge) {
  return function(yearOfBirth) {
    var a = " years left until retirement.";
    var age = 2019 - yearOfBirth;
    console.log(retirermentAge - age + a);
  };
}

var retirementUS = retirement(66);
var retirementAG = retirement(65);
var retirementIS = retirement(67);

retirementUS(1990);
retirementAG(1990);
retirementIS(1990);
```

```javascript
function interviewQuestion(job) {
  if (job === "designer") {
    return function(name) {
      console.log(name + ", can you explain what UX design is?");
    };
  } else if (job === "teacher") {
    return function(name) {
      console.log(name + ", What subject do you teach?");
    };
  } else {
    return function(name) {
      console.log("Hello, " + name + ", What do you do?");
    };
  }
}
```

```javascript
function interviewQuestion(job) {
  return function(name) {
    if (job === "desginer") {
      console.log(name + ", can you explain what UX design is?");
    } else if (job === "teacher") {
      console.log("What subject do you teach, " + name);
    } else {
      console.log("Hello, " + name + ", what do you do?");
    }
  };
}
```

#### bind, call and apply

```javascript
var john = {
  name: "John",
  age: 26,
  job: "teacher",
  presentation: function(style, timeOfDay) {
    if (style === "formal") {
      console.log(
        "Good " +
          timeOfDay +
          ", Ladies and gentlemen. I'm " +
          this.name +
          ", I'm a " +
          this.job +
          " and I'm " +
          this.age +
          " years old."
      );
    } else if (style === "friendly") {
      console.log(
        "Hey! What's up? I'm " +
          this.name +
          ", I'm a " +
          this.job +
          " and I'm " +
          this.age +
          " years old. Have a nice " +
          timeOfDay +
          "."
      );
    }
  }
};

var emily = {
  name: "Emily",
  age: 35,
  job: "designer"
};
john.presentation("formal", "morning");
john.presentation.call(emily, "friendly", "afternoon");
// john.presentation.apply(emily, ['friendly', 'afternoon']);

var johnFriendly = john.presentation.bind(john, "friendly");

johnFriendly("morning");
johnFriendly("night");

var emilyFormal = john.presentation.bind(emily, "formal");
emilyFormal("afternoon");

var years = [1990, 1965, 1937, 2005, 1998];

function arrayCalc(arr, fn) {
  var arrRes = [];
  for (var i = 0; i < arr.length; i++) {
    arrRes.push(fn(arr[i]));
  }

  return arrRes;
}

function calculateAge(el) {
  return 2019 - el;
}

function isFullAge(limit, el) {
  return el >= 18;
}

var ages = arrayCalc(years, calculateAge);
var fullJapan = arrayCalc(ages, isFullAge.bind(this, 20));
console.log(ages);
console.log(fullJapan);
```

[Back to Index](index.md)
