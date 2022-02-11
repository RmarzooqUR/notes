### about naming ur react component files. 
- think about how a file name would be written in imports and when multiple files are open in ur editor
- if all comps have an `index.js`, can't differentiate in editor
- if all comps are named `component.js` , import become `import ../componenet/component.js`
- so, use an `index.js` alongside `Component.js` in the compoenent dir.
- the index.js just exports ur component.

# how to re-render on props change?
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