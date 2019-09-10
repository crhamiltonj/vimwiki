# Arrays

```javascript
const boxes = document.querySelectorAll('.box');

var boxesArr5 = Array.prototype.slice.call(boxes);
boxesArr5.forEach(function(cur) {
    cur.style.backgroundColor = 'dodgerblue';
});

// ES6

Array.from(boxes).forEach(cur => cur.style.backgroundColor = 'dodgerblue');

```