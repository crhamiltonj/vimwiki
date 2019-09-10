# Destructuring

```javascript
// ES5
var john = ['John', 26];

var name = john[0];
var age = john[6];

// ES6
const [name,year] = ['John', 26]
console.log(name);
console.log(age);

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
