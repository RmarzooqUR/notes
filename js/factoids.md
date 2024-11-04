- `||` operator can return a value. 
  - returns RHS when LHS is falsy
- `??` operator
  - returns RHS when LHS is *null* or *undefined*
- `&&` operator
  - returns LHS when LHS is falsy
  - else returns RHS when LHS is truthy
 
## JS `new Function` syntax
- is not a closure
- turns strings into functions
- helpful where say an api response is returning some code and that needs to be executed on UI
```js
new Function('a', 'b', 'return a + b'); // basic syntax
```
