# Module Pattern

The module pattern allows you to create objects that keeps some data or methods private while allowing other data and methods to be public. It does this using [IIFE](javascript_functions_objects.md#Immediately_Invoked_Function_Expressions) and [closures](javascript_functions_objects.md#Closures).

```javascript
var budgetController = (function() {
  var x = 23;
  var add = function(a) {
    return x + a;
  };

  return {
    publicTest: function(b) {
      console.log(add(b));
    }
  };
})();
```

In the example above. x and the add() function are not accessible, but the publicTest function is.

[Back](javascript.md)
