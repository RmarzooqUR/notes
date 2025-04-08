# Custom Header
- You can create custom header components by passing it as part of the `framworkComponents` prop's dictionary
```js
import {AgCustomHeader} from './AgCustomHeader'
...
  frameworkComponets={{ AgCustomHeader: AgCustomHeader}}
...
```

- Ag-grid will pass some default props to the framworkComponents, `column` is one among them
- you can listen to events on the column (like filter, sort state of column) changed by user or `gridApi`
- this listener listens for changes on other columns CustomHeader component as well
  - useful when u need to make changes to column A, when something changes on column B (like sort)
 ```js

useEffect(()=> {
  column.addEventListener('sort', (e) => {
    if (e.api.getColumnState().sort !== column.getSortState())
      // rest sort state of column
  })
  return () => column.removeEventListener('sort', _..noop);
}, [])
```

# Advance Filter
