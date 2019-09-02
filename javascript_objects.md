# Objects and Methods

## Object Literals

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

## Object Methods

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

### Accessing members of an Object

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

[Back to JavaScript](javascript.md)
[Back to Index](index.md)
