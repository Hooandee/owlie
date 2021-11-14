# Javascript Fundamentals 📚

## Closures

A closure is a combination of a function bundled together (_enclosed_) with references to its sorroundings (_lexical environment_).

Closures are formed everytime a function is created at _**function creation time**_.

### Lexical Scoping

---

When a function is accessing to the external scope without defining the function within that is lexical scoping.

The parser resolves the variable nables when functions are nested.

```js
var name = "Juandi";

function alertName() {
  alert(name); // Closure is accessing the outer scope to resolve the variable
}
```

---

Everytime we invoke a function (closure) it will have access to the external scope defined on its creation time. That makes variables alive as long as the closure exists, **the closure carries the lexical environment over**.

#### Closure Example:

---

```js
// This is a function factory (pattern)
function makeAdder(x) {
  return function (y) {
    return x + y;
  };
}
```

We can instantiate two closures that will carry the lexical environment (_x variable value_):

```js
var add5 = makeAdder(5);
var add10 = makeAdder(10);

console.log(add5(2)); // prints 7
console.log(add10(5)); // prints 15
```

The important thing here is that we have two different closures with two different scopes, where the value of the lexical environment is `x = 5` and `x = 10`.

---

The closure paradigm parallels the object-oriented programming paradigm. Since javascript is an **event driven** language, closures are used as callabacks on events, like `onClick`, because they carry the logic and the context.

Thanks to closures we can create private method in javascript, something that is not possible by default. This allows `data hidding` and `encapsulation`.

```js
function makeCounter() {
  var privateCounter = 0;

  function changeBy(x) {
    return (privateCounter += x);
  }

  return {
    increment: function () {
      changeBy(1); // Closure 1
    },
    decrement: function () {
      changeBy(-1); // Closure 2
    },
    value: function () {
      return privateCounter;
    },
  };
}
```

And we instantiate closures:

```js
var counter1 = makeCounter();
var counter2 = makeCounter();

alert(counter1.value); // prints 0

counter2.increment();
alert(counter2.value); // prints 1

counter1.increment();
counter1.increment();
counter2.decrement();

alert(counter1.value); //  prints 2
alert(counter2.value); // prints 0
```

As we can see we have `hiden data` (counter value) and we are `encapsulating` functionality (exposed methods).
