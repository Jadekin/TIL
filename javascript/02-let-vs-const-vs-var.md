# `let` vs. `var` vs. `const`

There are three main ways to declare variables: var, let, and const, with their own characteristics and use cases.


## var 

 `var` was the original way to declare variables. They have function or global scope, can be reassigned and redeclared within their scope, and exhibit hoisting behavior, allowing them to be used before they are declared. However, during hoisting, `var` variables are initially assigned a value of undefined until they are explicitly assigned a value.

```javascript

function showVar() {
  console.log(x); // undefined
  var x = 100;
  if (true) {
    var x = 200;
    console.log(x); // 200
  }
  console.log(x); // 200
}

showVar();

```

## let

`let` was introduced in ES6 (ECMAScript 2015) and provides block scoping. Variables declared with `let` are limited in scope to the block in which they are defined. They can be reassigned within their scope but not redeclared. Unlike `var`, `let` variables are not hoisted, meaning they cannot be accessed before they are declared. This makes `let` a safer choice for variable declarations.

```javascript

function showLet() {
  console.log(x); // Reference error
  let x = 100;
  if (true) {
    let x = 200;
    console.log(x); // 200
  }
  console.log(x); // 100
}

showLet();

```

## const

`const` is also introduced in ES6 and stands for "constant." Variables declared with `const` are block-scoped like let, but they cannot be reassigned once they are assigned a value. However, it's important to note that `const` does not make objects or arrays immutable. Only the assignment of the variable itself is prevented.

```javascript

function showConst() {
  const x = 100;
  if (true) {
    const x = 200;
    console.log(x); // 200
  }
  console.log(x); // 100
}

showConst();

```

## Summary

|      | Scope         | Reassignment | Redeclaration | Hoisting | Initial Value  | Block-level | Use Promoted |
|------|---------------|--------------|---------------|----------|----------------|-------------|--------------|
| `var`    | Function/Global | Allowed      | Allowed       | Hoisted  | `undefined`    | No  | No            |
| `let`    | Block         | Allowed      | Not allowed   | Not hoisted | `undefined`   | Yes | Yes           |
| `const`  | Block         | Not allowed  | Not allowed   | Not hoisted | No initial value, must be assigned when declared | Yes | Yes           |
