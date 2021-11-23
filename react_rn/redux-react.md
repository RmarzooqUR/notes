# Terms
- **store** - where the global state is stored. A reducer is passed to the store.
- **reducer** - modifies the state based on incoming action's *type, payload*.
- **action** - a js object with `{ type, payload }` properties that are dispatched via the `store.dispatch` method.
- **dispatch** - the `store.dispatch` method that dispatches actions to store via reducer.


# Map store(state)/dispatch to props (React-redux)
- `mapStoretoPorps` takes 2 params `state, ownProps`
- `mapStoretoProps` must return an object.
- `mapStoretoProps` allows store to be passed as props to a react component
  - which can then be destructured as `const Component = ({ store }) => {}`
  - the `mapStoretoProps(store)` function returns the store or part of the store.
---
- `mapDispatchtoProps` can either be an object or function.
**As Object**
it contains values properties that are actionCreators and dispatch actions
```js
import {increment, decrement} from './actions'
const mapDispatchtoProps = {increment, decrement}
```
**As Function**
- should return a plain object.
- if `mapDispatchtoProps(dispatch)` isnt used in `connect`, `dispatch` is injected to component by default.
- `dispatch` is injected only for 
  - above condition
  - alongwith other action creators, it is returned in the `mapDispatchtoProps` function. 
```js
import {increment, decrement} from './actions'
const mapDispatchToProps = (dispatch, ownProps) => { return {increment:(data)=>dispatch(increment(data))}}
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

# Full Boilderplates
## non-react redux pattern
```js
// reducers.js
const reducer = (store, action){
  switch(action){
    case "case1": 
      return {
        ...state,
        data1:  action.payload
      }
    case default:
      return state;
  }
}
```
```js
// store
const store = createStore(reducer)
```
```js
// actions.js
const putBinary = (data) =>{
  return {type:"case1", payload:data}
}
```
```js
// usage
import putBinary from './actions'

const data = store.getState()
store.dispatch(putBinary("10001001"))
``` 
## connect api
- use `<Provider store={store}>` parent component to provide access to store.
```js
// usage
import putBinary from './actions'

const DataComponent = (props)=>{
  props.putBinary()   //dispatch putBinary action
  props.dispatch(putBinary())    //
  return <></>
}

const mapStateToProps = (state, ownProps) => {{data:state.specificData[ownProps.id]}}

const mapDispatchToProps = {putBinary}
const mapDispatchToProps = (dispatch, ownProps) => {{putBinary, dipatch}}
const mapDispatchToProps = (dispatch, ownProps) => {
  return { 
    putBinary: (binNo)=>dispatch(putBinary(binNo)),
    // dispatch     //injecting dispatch
  }
}
// use bindActionCreators to avoid rewriting dispatches
const mapDispatchtoProps = (dispatch) => {
  return bindActionCreators({putBinary}, dispatch);
}
// inject dispatch
const mapDispatchtoProps = (dispatch) => {
  return {...bindActionCreators({putBinary}, dispatch), dispatch};
}
```

## reduxjs/toolkit
[provided above](#procedure)
## redux thunk
## custom middleware