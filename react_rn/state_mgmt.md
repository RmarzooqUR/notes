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