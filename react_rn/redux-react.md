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
# Using @reduxjs/toolkit
- toolkit allows you to use redux pattern without using `mapStatetoProps`/`mapDispatchtoProps`
  - using hooks like `useSelector` and `useDispatch`
  - `useSelector` - allows you to fetch the complete state or part of the state.
  - `useDispatch` - returns the dispatch function and can be called within the component

## Procedure
- store is configured using `configureStore` and options object is passed with a reducer property
```js
import { configureStore } from '@reduxjs/toolkit'
import {reducer} from 'slice.js'

export default configureStore({
  reducer: {
      counter:reducer
  }
})
```
- **slice** allows you to create reducer functions without writing actions
  - slice is created with `createSlice` and options are passed
    - must contain `name`, `initialState`, at least 1 `reducer`, properties.
    - reducer is a function with `state` as its param
  - the `slice`'s properties `slice.reducer`, `slice.actions` can be exported
    - the actions can be passed to dispatch wherever required
```js
import { reducer } from 'slice.js'

const App = () => {
    const stat = useSelector(state=>state.item1.stat)
    const dispatch = useDispatch()
    //...
    dispatch(reducer())
}
```

# Async Actions
- any async logic is a side effect and redux doesnt handle side effects.
- therefore we write a middleware that intercepts an async action and dispatches it upon completion of the side effect.
## Redux Thunk

## Custom redux middleware