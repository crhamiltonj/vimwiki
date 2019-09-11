# Spread operator

The spread operator `...` will take the elements of an array and apply them to the input parameters of a function. It can also be used to join arrays into a single array.

## With Function Parameters

```javascript
function addFourAges(a, b, c, d) {
  return a + b + c + d;
}

// ES5
var sum1 = addFourAges(18, 30, 12, 21);
console.log(sum1);

var ages = [18, 30, 12, 21];
var sum2 = addFourAges.apply(null, ages);
console.log(sum2);

//ES6
const sum3 = addFourAges(...ages);
console.log(sum3);
```

## With Arrays

```javascript
const familySmith = ["John", "Jane", "Mark"];
const familyMiller = ["Mary", "Bob", "Ann"];
const bigFamily = [...familySmith, "Lily", ...familyMiller];
console.log(bigFamily);
```

## With NodeLists

```javascript
const h = document.querySelector("h1");
const boxes = document.querySelectorAll(".box");
const all = [h, ...boxes];
Array.from(all).forEach(cur => (cur.style.color = "purple"));
```

[Back](javascript__next_gen.md)
