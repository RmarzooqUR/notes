## useReducer vs Redux vs useContext
- useReducer returns a following object `[state, dispatch] = useReducer(someReducer, initialState)`
- it can't store a global state.
- there may be different reducers for states of different components.
- combining them into a single global state is not ideal.
---
- useContext can store a global state but doesnt follow the reducer pattern
---
- redux can have both a global state and reducer pattern
- but state has to be mapped to props and dispatch matched to props and use `connect(mapStateToProps, matchDispatchToProps)(Component)`

## useRef and refs
- `useRef` hooks create ref objects that can store state that doesn't update the state of a component
- refs are a crutch (react doc says escape hatch), to much of it in ur code means the code has disability
- due to the fact that how react manages refs, they shouldn't be accessed during render phase, (they are null of hold old value at render time). May make component behavior unpredictable (😮‍💨)
### `ref` prop
- react makes a `ref` prop available for components
- if the `ref` prop is assigned a object `xRef` created with `useRef` hook, its DOM element is assigned to `xRef.current` (done after commit phase of react applying changes (***react has a render & a commit phase***)).
  - now any browser apis can be used to manipulate this DOM element like `.focus(), scroll(), prepend()` etc. 
- if the `ref` prop is assigned a function (takes `node` as param), the `xRef` can contain dynamic no of elements as Map, array or object etc of DOM nodes, which can then be manipulated from single ref object.
```jsx
const Mycomponent = () => {
  const xRef = useRef<Map>()

  return <>
    <div ref={(node) => {
      xRef.current.set(key, node)
      return () => {
        xRef.current.delete(key)
      }
    }}></div>
  </>
}
```
- don't use destructuctive dom apis (`remove()` etc), may interfere with changes to DOM that react makes
