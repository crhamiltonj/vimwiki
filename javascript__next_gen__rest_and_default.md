# Rest and Default Parameters

Rest parameters allow us to pass an arbitrary number of parameter to a function.

## Arbitrary arguments

```javascript
// ES5

function isFullAge5() {
  console.log(arguments);

  var argsArr = Array.prototype.slice.call(arguments);
  argsArr.forEach(function(cur) {
    console.log(2019 - cur >= 18);
  });
}

isFullAge5(1990, 1999, 1965);
isFullAge5(1990, 1999, 1965, 2016, 1987);

// ES6
function isFullAge6(...years) {
  console.log(years);
  years.forEach(cur => console.log(2019 - cur >= 18));
}

isFullAge6(1990, 1999, 1965);
isFullAge6(1990, 1999, 1965, 2016, 1987);
```

## Required Parameters

```javascript
// ES5

function isFullAge5(limit) {
  console.log(arguments);

  var argsArr = Array.prototype.slice.call(arguments, 1);
  argsArr.forEach(function(cur) {
    console.log(2019 - cur >= limit);
  });
}

isFullAge5(21, 1990, 1999, 1965);
isFullAge5(1990, 1999, 1965, 2016, 1987);

// ES6
function isFullAge6(limit, ...years) {
  console.log(years);
  years.forEach(cur => console.log(2019 - cur >= limit));
}

isFullAge6(1990, 1999, 1965);
isFullAge6(1990, 1999, 1965, 2016, 1987);
```

## Default Parameters

In ES5 defaults are specified inside the function with ternary operators.

### ES5

```javascript
// ES5

function SmithPerson(firstName, yearOfBirth, lastName, nationality) {
  lastName === undefined ? (lastName = "Smith") : (lastName = lastName);
  nationality === undefined
    ? (nationality = "American")
    : (nationality = nationality);

  this.firstName = firstName;
  this.lastName = lastName;
  this.yearOfBirth = yearOfBirth;
  this.nationality = nationality;
}

var john = new SmithPerson("John", 1990);
var emily = new SmithPerson("Emily", 1983, "Diaz", "spanish");
```

### ES6

In ES6 defaults are specified in the parameter list.

```javascript
// ES6

function SmithPerson(
  firstName,
  yearOfBirth,
  lastName = "Smith",
  nationality = "american"
) {
  this.firstName = firstName;
  this.lastName = lastName;
  this.yearOfBirth = yearOfBirth;
  this.nationality = nationality;
}

var john = new SmithPerson("John", 1990);
var emily = new SmithPerson("Emily", 1983, "Diaz", "spanish");
```

[Back](javascript__next_gen.md)
