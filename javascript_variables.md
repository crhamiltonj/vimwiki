# Variables

A container to store a value that you can use over and over

## To declare a variable

```javascript
var firstName = "John";
```

- Use the var keyword to tell javascript that you are creating a variable
- the item on the left side is the name of the variable
- the item on the right side is the value the variable contains

## Datatypes

- Number: Floating point numbers for decimals and integers
- String: Sequence of characters, used for text
- Boolean: Logical data type that can only be `true` or `false`
- Undefined: Data type of a variable that does not have a value yet
- Null: Also means 'non-existant`

Javascript has dynamic typing: data types are automatically assigned to variables

## Variable Names

- Variable names should be descriptive
- Javascript convention is to use camelCase variable names
  - the first letter is lowercase
  - each following word the first letter is uppercase

### Rules

- Variables cannot start or contain characters with numbers or symbols that are not \\_ or \$
- Reserved JavaScript keywords cannot be used as variable names

## Variable Mutation and Type Coercion

- Type Coercion -- JavaScript automatically converts certain variables so that the can be combined with other variables of another type.
- Variable Mutation -- JavaScript will also convert the type of a variable upon reassignment with a different type.
