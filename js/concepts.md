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
  - returns object with `value` and `done` properties
  - a true value of `done` implies that the generator has finished.
- return(value)
  - if preemptive completion of generator is required.
  - it returns the value param and completes the generator. Can be called after generator has finished too
- 
### passing parameters to next(param)
- if a var in generator func is assigned a yield expression. the param is assigned to the var.

![Passing Params to generator function](./Screenshot%20(2).png)