# Basic Language Features

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

- Variables cannot start or contain characters with numbers or symbols that are not \\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\_ or \$
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

[Back](javascript.md)
