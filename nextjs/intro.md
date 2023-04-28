# Introduction
React is a library, next is a **framework** providing
- a router
- a state management solution

for [next 13 vs older](./next13vsOld.md), this notes provides details of Next 13

# layout.js , head.js, page.js
or `.jsx` / `.tsx`
These are special files with special functions and use cases for Next including for serverside rendering

## `page.js`
- this is the primary UI component of a route. 
- a route needs to have a `page.js` in order for the route to be publicly accessible
  - this means we can add directories that are not accessible to public as well

## `layout.js`
- when some UI layout is shared b/w multiple routes (think sidebar/navbar)
  - we can define them in a layout.js
- layout components accept a children prop & render it whereever required in the layout's UI definiton
- the layout at root is called RootLayout
```jsx
// layout.js
export default RootLayout = ({ children }) => {
  return (
    <html>  {/* THE ROOT LAYOUT MUST BE ENCAPSULATED INSIDE AN HTML TAG*/}
      <TopBar />
      <SideBar />
      {children}
    </html>
  )
}
```
- when using `app` the root directory must have a root layout.
- props can't be passed from parent layout to child layouts
## `head.js`
- We can define the `<head>` element of a page through this like `<title>, <meta>` etc
- the component defining it must
  - enclose it in a React.Fragment - `<></>`

# Routes
- Routing in NextJS is done with directory structure. 
- a directory with `page.js` is publicly accessible
- to create UI on route, export a default React component
- more details (here)[./routes.md]
