# Strings in ES6

## Template Literals

```javascript
let firstName = 'John';
let lastName = 'Smith';
const yearOfBirth = 1990;
function calcAge(year) {
    return 2019 - year;
}

// es5
console.log('This is ' + firstName + ' ' + lastName + '. He was born in ' + yearOfBirth + '. Today he is ' + calcAge(yearOfBirth) + ' years old.');

// es6
console.log(`This is ${firstName} ${lastName}. He was born in ${yearOfBirth} and is ${calcAge(yearOfBirth)} years old.`);

// string.startsWith('str')
const n = `${firstName} ${lastName}`

console.log(n.startsWith('J')); // true
console.log(n.startsWith('n')); // false
console.log(n.startsWith('j')); // false

// string.endsWIth('str')
const n = `${firstName} ${lastName}`

console.log(n.endsWith('th')); // true
console.log(n.endsWith('Sm')); // false
console.log(n.endsWith('TH')); // false

// string.includes('str')
const n = `${firstName} ${lastName}`

console.log(n.includes(' ')); // true
console.log(n.includes('ohn SM')); // true
console.log(n.includes('mit')); // true

//string.repeat(n)

console.log(firstName.repeat(5));
```

[Back](javascript__next_gen.md)