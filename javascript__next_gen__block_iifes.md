# Blocks and IIFEs

## Block Expression

```javascript
{
    const a =1;
    const b =2;
    var c =3;
}

console.log(a + b);

// will succeed because c is part of the same function (the whole file in this case)
console.log(c)
```

## IIFE
```javascript
(function() {
    var c = 3
})();

console.log(c);
```

[Back](javascript__next_gen.md)
