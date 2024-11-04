# Generator functions
- `Generator` is a type in js
- cant be instantiated directly 
- returned by generator functions
```js
function* generator(){
  yield 1;
  yield 2;
}

const gen = generator() // gen is now a Generator object
```
## generator methods
- next() method
  - runs till the next yield statement 
  - returns object with `value` and `done` properties
  - a true value of `done` implies that the generator has finished.
- return(value)
  - if preemptive completion of generator is required.
  - it returns the value param and completes the generator. Can be called after generator has finished too
- 
### passing parameters to next(param)
- if a var in generator func is assigned a yield expression. the param is assigned to the var.

![Passing Params to generator function](./Screenshot%20(2).png)


# Closures & Currying
In practice gives reusable, maintainable code
## Closure
- A closure is a function that has access to its parent scopes local functions even after the parent function is finished executing
- its a trick to define private variables in JS (b4 es6)
- Closure is acheived by returning a function from inside a parent function
## Currying
- Chaining of closures gives function currying
- ~much like the call `f(g(h(x)))`~ (<- this is function composition) - js equiv -> someFn(x)(y)(z)
```js
// Closure
function countXFrom10(prim) {
  var loc = 10
  return function (seco) {
    // could also implement a loop for count x times from 10
    loc=loc+prim+sec
    return loc
  }
}

let count1From10 = countXfrom(1)
let count10From10 = countXfrom(10)
count1from10(12)
count10from10(15)

// Currying
function some(x) {
  // ...
  return function (y) {
    // ...
    return function (z) {
      // ...
    }
  }
}

some(10)(11)(12)
```
