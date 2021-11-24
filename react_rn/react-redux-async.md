# Async actions in Redux
Side effects in redux action creators is not supported
- redux toolkit `configureStore` functions automatically adds thunk middleware

## redux thunk
apply thunk like this
```js
const store = createStore(reducers, applyMiddleware(thunk))
```
- action creators return a function which when has a return, its a promise.
- this returned function dispatches the action
```js
const newAciton = (data) => {
  return function func(dispatch){
    axios.get('url?'+data)
      .then((data)=>{
        dispatch({'newAction', data})
      })
  }
}
```
## custom middleware