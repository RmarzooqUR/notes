# Terms
- **store** - where the global state is stored. A reducer is passed to the store.
- **reducer** - modifies the state based on incoming action's *type, payload*.
- **action** - a js object with `{ type, payload }` properties that are dispatched via the `store.dispatch` method.
- **dispatch** - the `store.dispatch` method that dispatches actions to store via reducer.


# Map store(state)/dispatch to props (React-redux)
- `mapStoretoProps` allows store to be passed as props to a react component
  - which can then be destructured as `const Component = ({ store }) => {}`
  - the `mapStoretoProps(store)` function returns the store or part of the store.
- `mapDispatchtoProps(dispatch)` makes dispatch available to props via a returned callback.
```js
const mapDispatchToProps(dispatch) => {
    return {
        handleDispatch(data){
            dispatch({type:'someActionType',payload:data})
        }
    }
}

```