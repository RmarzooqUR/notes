# Hooks
Hooks are used for
- extracting repetitive code out of a component tree
- have a cleaner state management api


- different instances of the same hook don't share internal states & methods (even in the same component)
  - like private properties of objects of a class

- you can chain the reponse of one hook by passing it to another hook

- we can think of hooks as wrapper around the logic they enclose
- any states/effects described inside the hook are **part of the component** where the hook is invoked