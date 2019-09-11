# Maps

Maps have the following features

- Can use anything as keys
- Maps are iterable
- easy to get the size with the size property
- You can easily add or remove elements to a map

```javascript
const question = new Map();
question.set(
  "question",
  "What is the official name of the latest major version of javascript?"
);
question.set(1, "ES5");
question.set(2, "ES6");
question.set(3, "ES2015");
question.set(4, "ES7");
question.set("correct", 3);
question.set(true, "Correct Answer");
question.set(false, "Wrong, please try again.");

console.log(question.get("question"));
console.log(question.size);

if (question.has(4)) {
  question.delete(4);
}

question.clear();

questtion.forEach((value, key) =>
  console.log(`This is ${key} and it's set to ${value}`)
);

for (let key of question) {
  // process key
  console.log(`This is ${key}`);
}

for ([key, entry] of question.entries()) {
  // process key and entry
  console.log(`This is ${key} and it's set to ${value}`);
}

for ([key, value] of question.entries()) {
  // process key and entry
  console.log(`This is ${key} and it's set to ${value}`);
  if (typeof(key) === 'number){
    console.log(`This is ${key} and it's set to ${value}`);
  }
}

const ans = parseInt(prompt('Write the correct))
console.log(question.get(ans === question.get('correct')))
```

[Back](javascript__next_gen.md)
