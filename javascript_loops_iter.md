# Loops and Iteration

## for Loops

```javascript
for (i = 0; i < 10; i++) {
  console.log(i);
}

// i = 0, 0 < 10 true, log i to console, add 1 to i
// i = 1, 1 < 10 true, log i to console, add 1 to i
// ...
// i = 9, 9 < 10 true, log i to console, add 1 to i
// i = 10, 10 < 10 false, exit loop

var john = ["John", "Smith", 1990, "designer", false];

for (i = 0; i < john.length; i++) {
  console.log(john[i]);
}

// i=0, 0 < john.length true, log john[0] to console, add 1 to i
// i=1, 1 < john.length true, log john[1] to console, add 1 to i
// ...
// i=4, 4 < john.length true, log john[4] to console, add 1 to i
// i=5, 5 < john.length false, exit the loop
```

## while Loops

```javascript
var i = 0;
while (i < john.length) {
  console.log(john[i]);
}
```

## continue and break Statements

### continue

Stops processing this iteration of the loop and starts again at the next iteration.

```javascript
var john = ["John", "Smith", 1990, "designer", false];

for (i = 0; i < john.length; i++) {
  if (typeof (john[i] !== "string")) continue;
  console.log(john[i]);
}
```

### break

Stops processing the loops and end further iterations.

```javascript
var john = ["John", "Smith", 1990, "designer", false];

for (i = 0; i < john.length; i++) {
  if (typeof (john[i] !== "string")) break;
  console.log(john[i]);
}
```

### Looping Backwards

```javascript
for (var i = john.length - 1; i >= 0; i--) {
  console.log(john[i]);
}
```

[Back](javascript.md)
