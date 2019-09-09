# Functions and Objects

## Function Constructor

```javascript
var john = {
  name: "John",
  yearOfBirth: 1990,
  job: "teacher"
};

var Person = function(name, yearOfBirth, job) {
  this.name = name;
  this.yearOfBirth = yearOfBirth;
  this.job = job;
};

Person.prototype.calculateAge = function() {
  console.log(2019 - this.yearOfBirth);
};

Person.prototype.lastName = "Smith";

var john = new Person("John", 1990, "teacher");
var jane = new Person("Jane", 1969, "designer");
var mark = new Person("Mark", 1948, "retired");

john.calculateAge();
jane.calculateAge();
mark.calculateAge();

console.log(john.lastName);
console.log(jane.lastName);
console.log(mark.lastName);
```

## Object.create

```javascript
var personProto = {
  calculateAge: function() {
    console.log(2019 - this.yearOfBirth);
  }
};

var john = Object.create(personProto);

john.name = "John";
john.yearOfBirth = 1990;
john.job = "teacher";

var jane = Object.create(personProto, {
  name: { value: "Jane" },
  yearOfBirth: { value: 1990 },
  job: { value: "designer" }
});
```

## Primitives vs Objects

### Primitives

```javascript
var a = 23;
var b = a;
a = 46;

console.log(a);
console.log(b);
```

### Objects

```javascript
var obj1 = {
  name: "John",
  age: 26
};

var obj2 = obj1;

obj1.age = 30;
console.log(obj1);
console.log(obj2);
```

### Using Objects with functions

```javascript
var age = 27;
var obj = {
  name: "Jonas",
  city: "Lisbon"
};

function change(a, b) {
  a = 30;
  b.city = "San Francisco";
}

change(age, obj);
console.log(age);
console.log(obj.city);
```

### Passing functions as arguments

```javascript
var years = [1990, 1965, 1937, 2005, 1998];

function arrayCalc(arr, fn) {
  var arrRes = [];

  for (var i = 0; i < arr.length; i++) {
    arrRes.push(fn(arr[i]));
  }

  return arrRes;
}

function calculateAge(el) {
  return 2019 - el;
}

function isFullAge(el) {
  return el >= 18;
}

function maxHeartRate(el) {
  if (el >= 18 && el <= 81) {
    return Math.round(206.9 - 0.67 * el);
  } else {
    return -1;
  }
}

var ages = arrayCalc(years, calculateAge);
var fullAges = arrayCalc(ages, isFullAge);
var maxHeartRates = arrayCalc(ages, maxHeartRate);
console.log(ages);
console.log(fullAges);
console.log(maxHeartRates);
```

### Functions returning functions

```javascript
function interviewQuestion(job) {
  if (job === "designer") {
    return function(name) {
      console.log(name + ", can you explain what UX design is?");
    };
  } else if (job === "teacher") {
    return function(name) {
      console.log(name + ", What subject do you teach?");
    };
  } else {
    return function(name) {
      console.log("Hello, " + name + ", What do you do?");
    };
  }
}

var teacherQuestion = interviewQuestion("teacher");
var designerQuestion = interviewQuestion("designer");
teacherQuestion("John");
designerQuestion("John");
interviewQuestion()("Mark");
```

### Immediately Invoked Function Expressions

Immediately Invoked Function Expressions (IIFE) creates a function that provides data hiding to the data and methods inside of the expression.

```javascript
function game() {
  var score = Math.random() * 10;
  console.log(score >= 5);
}

game();

(function() {
  var score = Math.random() * 10;
  console.log(score >= 5);
})();

(function(goodLuck) {
  var score = Math.random() * 10;
  console.log(score >= 5 - goodLuck);
})(5);
```

### Closures

Closures are functions that return another function where the inputs can be customized and saved and then assigned to another variable that retains the customization. The resulting function that is returned can no be called with previously expressed default values. The inner function also has access to the surrounding data and methods because of scoping rules.

```javascript
function retirement(retirermentAge) {
  return function(yearOfBirth) {
    var a = " years left until retirement.";
    var age = 2019 - yearOfBirth;
    console.log(retirermentAge - age + a);
  };
}

var retirementUS = retirement(66);
var retirementAG = retirement(65);
var retirementIS = retirement(67);

retirementUS(1990);
retirementAG(1990);
retirementIS(1990);
```

```javascript
function interviewQuestion(job) {
  if (job === "designer") {
    return function(name) {
      console.log(name + ", can you explain what UX design is?");
    };
  } else if (job === "teacher") {
    return function(name) {
      console.log(name + ", What subject do you teach?");
    };
  } else {
    return function(name) {
      console.log("Hello, " + name + ", What do you do?");
    };
  }
}
```

```javascript
function interviewQuestion(job) {
  return function(name) {
    if (job === "desginer") {
      console.log(name + ", can you explain what UX design is?");
    } else if (job === "teacher") {
      console.log("What subject do you teach, " + name);
    } else {
      console.log("Hello, " + name + ", what do you do?");
    }
  };
}
```

### bind, call and apply

```javascript
var john = {
  name: "John",
  age: 26,
  job: "teacher",
  presentation: function(style, timeOfDay) {
    if (style === "formal") {
      console.log(
        "Good " +
          timeOfDay +
          ", Ladies and gentlemen. I'm " +
          this.name +
          ", I'm a " +
          this.job +
          " and I'm " +
          this.age +
          " years old."
      );
    } else if (style === "friendly") {
      console.log(
        "Hey! What's up? I'm " +
          this.name +
          ", I'm a " +
          this.job +
          " and I'm " +
          this.age +
          " years old. Have a nice " +
          timeOfDay +
          "."
      );
    }
  }
};

var emily = {
  name: "Emily",
  age: 35,
  job: "designer"
};
john.presentation("formal", "morning");
john.presentation.call(emily, "friendly", "afternoon");
// john.presentation.apply(emily, ['friendly', 'afternoon']);

var johnFriendly = john.presentation.bind(john, "friendly");

johnFriendly("morning");
johnFriendly("night");

var emilyFormal = john.presentation.bind(emily, "formal");
emilyFormal("afternoon");

var years = [1990, 1965, 1937, 2005, 1998];

function arrayCalc(arr, fn) {
  var arrRes = [];
  for (var i = 0; i < arr.length; i++) {
    arrRes.push(fn(arr[i]));
  }

  return arrRes;
}

function calculateAge(el) {
  return 2019 - el;
}

function isFullAge(limit, el) {
  return el >= 18;
}

var ages = arrayCalc(years, calculateAge);
var fullJapan = arrayCalc(ages, isFullAge.bind(this, 20));
console.log(ages);
console.log(fullJapan);
```

[Back](javascript.md)
