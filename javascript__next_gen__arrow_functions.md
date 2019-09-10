# Arrow functions

Arrow functions streamlines simple callback functions by eliminating the need for the function keyword, the parens, the curly braces and the return keyword.

These features may need to be added back as the arrow function grows in complexity.

```javascript
const years = [1990, 1965, 1982, 1937];

// ES5

var  ages5 = years.map(function(el) {
    return 2016 - el;
})

console.log(ages5);

// ES6

// one parameter, one statement
let ages6 = years.map(el => 2019 - el);
console.log(ages6)

// multiple parameters, one statement
ages6 = years.map((el, index) => `Age element ${index +1}: ${2019 -el}.`);
console.log(ages6);

// multiple parameters, multiple statements
ages6 = years.map((el, index) => {
    const now = new Date.getFullYear();
    const age = now - el;
    return  `Age element ${index +1}: ${age}.`;
})
console.log(ages6)

```

## Arrow functions and Lexical `this` keyword

Arrow function do not have their own `this` keyword.  They use the `this` keyword of the surrounding function.

```javascript

// ES5
var box5 = {
    color: green,
    position: 1,
    clickMe: function() {
        // This is needed so the inner function on the callBack can have access to the object's (box5) properties
        var self = this;
        document.querySelector('.green').addEventListener('click', function() {
            var str = 'This is box number ' + self.position + ' and it is ' + self.color;
            alert(str);
        })
    }
}
box5.clickMe();

// ES6
const box6 = {
    color: green,
    position: 1,
    clickMe: function() {
        // arrow functions can access the outer object's this
        document.querySelector('.green').addEventListener('click', () => {
            const str = 'This is box number ' + this.position + ' and it is ' + this.color;
            alert(str);
        })
    }
}
box6.clickMe();

```

## Using Arrow functions to clean up prototype functions

```javascript
function Person(name) {
    this.name = name;
}

//ES5

Person.prototype.myFriends5 = 
function(friends) {
    var arr = friends.map(function(el){
        return this.name + ' is friends with ' + el
    }.bind(this));

    console.log(arr);
}

var friends = ['Bob', 'Jane', 'Mark'];

new Person('John').myFriends5(friends);

// ES6

Person.prototype.myFriends5 = 
function(friends) {
    var arr = friends.map(el => `${this.name} is friends with ${el}`);
    console.log(arr);
}

new Person('Mike').myFriends6(friends);
```

[Back](javascript__next_gen.md)