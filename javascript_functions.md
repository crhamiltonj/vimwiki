# Functions

## Defining and calling functions

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

[Back to JavaScript](javascript.md)
[Back to Index](index.md)
