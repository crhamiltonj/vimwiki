# Classes

Classes are syntatic sugar for function constructors. Classes are not hoisted. Properties cannot be added to a class.

```javascript
//  ES5

var Person5 = function(name, yearOfBirth, job) {
  this.name = name;
  this.yearOfBirth = yearOfBirth;
  this.job = job;
};

Person5.prototype.calculateAge = function() {
  var age = new Date().getFullYear() - this.yearOfBirth;
};

var john5 = new Person("John", 1990, "teacher");

//ES6

class Person6 {
  constructor(name, yearOfBirth, job) {
    this.name = name;
    this.yearOfBirth = yearOfBirth;
    this.job = job;
  }

  calculateAge() {
    var age = new Date().getFullYear() - this.yearOfBirth;
  }
}

const john6 = new Person6("John", 1990, "teacher");
```

## Static Methods

```javascript
class Person6 {
  constructor(name, yearOfBirth, job) {
    this.name = name;
    this.yearOfBirth = yearOfBirth;
    this.job = job;
  }

  calculateAge() {
    var age = new Date().getFullYear() - this.yearOfBirth;
  }

  static greeting() {
    console.log("Hey there!");
  }
}

const john6 = new Person6("John", 1990, "teacher");
Person6.greeting();
```

## Subclasses

```javascript
var Person5 = function(name, yearOfBirth, job) {
  this.name = name;
  this.yearOfBirth = yearOfBirth;
  this.job = job;
};

Person5.prototype.calculateAge = function() {
  var age = new Date().getFullYear() - this.yearOfBirth;
};

var Athelete5 = function(name, yearOfBirth, job, olympicGames, medals) {
  Person5.call(this, name, yearOfBirth, job);
  this.olympicGames = olympicGames;
  this.medals = medals;
};

Athelete5.prototype = Object.create(Person5.prototype);
var johnAthelete5 = new Athelete5("John", "1990", "swimmer", 3, 10);

Athelete5.prototype.wonMedal = function() {
  this.medals++;
  console.log(this.medals);
};

// ES6

class Person6 {
  constructor(name, yearOfBirth, job) {
    this.name = name;
    this.yearOfBirth = yearOfBirth;
    this.job = job;
  }

  calculateAge() {
    var age = new Date().getFullYear() - this.yearOfBirth;
  }
}

class Athelete6 extends Person6 {
  constructor(name, yearOfBirth, job, olympicGames, medals) {
    super(name, yearOfBirth, job);
    this.olympicGames = olympicGames;
    this.medals = models;
  }

  wonMedal() {
    this.medals++;
    console.log(this.medals);
  }
}

const johnAthelete6 = new Athelete6("John", 1990, "swimmer", 3, 10);
johnAthelete.wonMedal();
johnAthelete.calculateAge();
```

[Back](javascript__next_gen.md);
