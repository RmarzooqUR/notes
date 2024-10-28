- [About naming ur react component files.](#about-naming-ur-react-component-files)
- [How to re-render on props change?](#how-to-re-render-on-props-change)
- [Cleanup method in useEffect](#cleanup-method-in-useeffect)
  - [Example](#example)
    - [**Senario** -](#senario--)
    - [**Solution**](#solution)
- [`useEffect` as lifecycle methods \& some pitfalls](#useeffect-as-lifecycle-methods--some-pitfalls)
- [Dotenv](#dotenv)

# About naming ur react component files. 
- think about how a file name would be written in imports and when multiple files are open in ur editor
- if all comps have an `index.js`, can't differentiate in editor
- if all comps are named `component.js` , import become `import ../componenet/component.js`
- so, use an `index.js` alongside `Component.js` in the compoenent dir.
- the index.js just exports ur component.

# How to re-render on props change?
- use the useEffect / [useDeepCompare](https://github.com/kentcdodds/use-deep-compare-effect)[when props are objects] hooks.
- re-render on porps change will not happen here, as the state has its own copy now
```js
const App = ( { props } ) => {
  const [state, setState] = useState(props)
}
```
- soln
```js
const App = ( { props } ) => {
  useEffect(()=>{

  }, [props])
}
```

# Cleanup method in useEffect
```js
useEffect(() => { 
  // do something
  return () => { /*cleanup*/ } // cleanup function
}, [])
```
- react performs a cleanup after a component is unmounted or the next effect is run
  - we need to provide the cleanup function in order for react to perform it
- useEffects of this type help in relieving memory and preventing memory leaks in the appln.

## Example
React throws error when the application tries to set state of an unmounted component

### **Senario** - 
You click a button which runs an effect which fetches data(not preferable - use hooks/event methods)
1. -> but you perform another action before the fetch completes
2. -> component is unmounted
3. -> the success of fetch tries to update the state of unmounted component
4. -> error
### **Solution**
add a request abort in the cleanup function
```js
// using axios to fetch
const [data, setData] = useState()
useEffect(() => {
  const src = axios.CancelToken.source()  // signal to axios that fetch was cancelled
  axios.get({ cancelToken: src.token })
    .then((data) => setData(data))
    .catch((err) => {
      if (err == axios.isCancel()){
        console.log(err)
      } else {/* handle api error */}
    })

  // cleanup function which runs on unmount (aborting the fetch)
  return () => {
    src.cancel()
  }
})

```
# `useEffect` as lifecycle methods & some pitfalls
- default behavior of useEffect is infinte loop
`useEffect(() => setSomeState(), [someState])` results in infinite loops

- useEffect *can be used* as a lifecycle method but it is not intended for that. 
```js
// componentDidMount
useEffect(() => { /*do something */ } , [])

// componentDidUpdate
useEffect(() => { /* do something */}, [ someState ])

// componentDidUnmount
useEffect(() => { 
  return () => { /*cleanup*/ } // cleanup function
}, [])
```

# Dotenv
- CRA internally uses `dotenv` pkg for managing environment variables
- or you can create a `.env` file & use `process.env.REACT_APP_<ENVVARNAME>` directly in your app
- or multiple files like `.env.development`, `.env.prod` etc can be created
  - and used as 
    - `npm start:.env.development`
    - `npm build:.env.prod`


# [Higher Order Components](https://legacy.reactjs.org/docs/higher-order-components.html)
- are wrapper components, can be used on components that have similar implementation
  - Ex. an `itemList` & an `itemComponent` need not have to be 2 compnents if they fetch from different sources
  - we can pass the individual datasource in the wrapper as prop and the wrapper returns a component
- [HOC is a pure function](https://legacy.reactjs.org/docs/higher-order-components.html#:~:text=A%20HOC%20is%20a%20pure%20function%20with%20zero%20side%2Deffects)
- 
