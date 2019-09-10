# Variable Declarations

let and const replace the var keyword for variable declarations in ES6.

- `let` -- replaces var for values that might change (mutate)
- `const` -- is used for values that are not expected to change over the course of a program run.

```javascript
// let and const

//es5
var name5 = 'Jane Smith';
var age5 = 23;
name5 = 'Jane Miller';
console.log(name5);

//es6 
const name6 = 'Jane Smith';
let age = 23;
// will throw an error
name6 = 'Jane Miller';
console.log(name6);
```

- Other Changes
  - var is function scoped
  - let and const are block scoped

In ES6 to use variables outside of a block, declare the variables outside of the block, where then you can define them inside of the block for let. for const the variable must be declared and defined outside of the block.  

```javascript
// es5
function driversLicense5(passedTest) {
    if (passedTest) {
        var firstName = 'John';
        var yearOfBirth = 1990;
    }
    // in es5 this line will succeed -- all variables in the same function are available
    console.log(firstname + ', born in ' + yearOfBirth + ' , is now officially allowed to drive a car.');
}

driversLicense5(true);

// es6
function driversLicense6(passedTest) {
    if (passedTest) {
        let firstName = 'John';
        const yearOfBirth = 1990;
    }
    // in es6 this line will fail -- only variables accessed in the same block {} are available, out side of the block they are undefined.
     console.log(firstname + ', born in ' + yearOfBirth + ' , is now officially allowed to drive a car.');
}

driversLicense6(true);
```
[Back](javascript__next_gen.md)