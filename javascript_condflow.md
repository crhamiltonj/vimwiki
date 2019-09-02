# Conditionals and Flow Control

## if / else Statements

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

## Boolean Logic

- `&&` - Logical AND - Returns `true` if both sides of expression are true
  and `false` if either side is false
- `||` - Logical OR - Return true if left side is true
- `!` - Logical NOT - Invert the true or false value

## Ternary Operator

Evaluates a test condition and returns a value base on whether the test is true or false

```javascript
var firstName = "John";
var age = 16;

age >= 18
  ? console.log(firstName + " drinks beer")
  : console.log(firstName + " drinks juice.");
```

## Switch Statements

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

## Truthy and Falsy Values

- falsy values evaluate to false in an expression

  - `undefined`
  - `null`
  - `0`
  - `''` (empty string)
  - `NaN` (Not a Number)

- truthy values evaluate to true in an expression: **_any value that is not falsy_**

## Equality Operators

- `==` Equality check with type coercion
- `===` Equality check with strict type checking

[Back to Javascript](javascript.md)
[Back to Index](index.md)
