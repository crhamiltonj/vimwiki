# Destructuring

## Desctructuring arrays

ES5 you have to get each element individually and store it to a variable

```javascript
// ES5
var john = ['John', 26];

var name = john[0];
var age = john[6];
```

ES6 you can specify all the elements and one time and each on will be put in the right place.

```javascript
// ES6
const [name,year] = ['John', 26]
console.log(name);
console.log(age);
```

## Desctructuring objects

```javascript

const obj = {
    firstName: 'John',
    lastName: 'Smith'
};

const {firstName, lastName} = obj;
console.log(firstName);
console.log(lastName);

// Use different variable names than the object provides
const {firstName: a, lastName: b} = obj;
console.log(a);
console.log(b);

```

## Returning multiple values from a function

```javascript
function calcAgeRetirement(year) {
    const age = new Date.getFullYear() - year;
    return [age, 65-age]
}

const [age, retirement] = calcAgeRetirement(1990);
console.log(age);
console.log(retirement);
```

[Back](javascript__next_gen.md)