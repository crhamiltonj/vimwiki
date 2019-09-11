# Arrays

## Traversing a NodeList

```javascript
const boxes = document.querySelectorAll(".box");

var boxesArr5 = Array.prototype.slice.call(boxes);
boxesArr5.forEach(function(cur) {
  cur.style.backgroundColor = "dodgerblue";
});

// ES6

const boxesArr6 = Array.from(boxes);
Array.from(boxes).forEach(cur => (cur.style.backgroundColor = "dodgerblue"));
```

## Looping

```javascript
// ES5
const boxes = document.querySelectorAll(".box");

var boxesArr5 = Array.prototype.slice.call(boxes);
boxesArr5.forEach(function(cur) {
  cur.style.backgroundColor = "dodgerblue";
});

for (var i = 0; i < boxesArr5.length; i++) {
    if (boxesArr5[i].className === 'box blue') {
        continue;
        // or break;
    }

    boxesArr5[i]. textContent = 'I changed to blue';
}

//ES6
const boxesArr6 = Array.from(boxes);

for const cur or boxesArr6) {
    if (cur.className.includes('blue')) {
        continue;
        // or break;
    }

    cur.textContent = 'I changed to blue!';
}

```

## Find Elements in an Array

```javascript
// ES5
var ages = [12. 17, 8, 21, 14, 11];
var full = ages.map(function(cur) {
    return  cur >= 18;
})

console.log(full);

console.log(full.indexOf(true));
console.log(ages[full.indexOf(true)]);

// ES6

console.log(ages.findIndex(cur => cur >= 18));
console.log(ages.find(cur => cur >=18));



```

[Back](javascript__next_gen.md)
