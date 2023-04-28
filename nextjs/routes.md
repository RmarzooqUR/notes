# Intro
- the directory structure directly maps to the route structure of the app.
- however this pattern can be broken out of through route groups

# Route Groups
Next provides this feature not as part of any implementation but for project organisation.
this is done by using parenthesis : (`(group_name)`) over our organising directory
```js
app
  | - (app)
        | - layout.js
        | - home
              | - page.js
        | - emails
              | - page.js
  | - (admin)
        | - layout.js   // different layout for different apps in same project
        | - dashboard
              | - page.js

```
This helps in- 
- Organising components without changing their routes
- Opting for completely different root layouts for parts that have completely different UI
- sharing layouts - the /home & /email would have a seperate layout for each if they weren't in a route group

# Dynamic routes
wrapping a route name in square brackets parameterises it with folder name as the param name: `[id]`

## Catch All & Optional catch all segments
- `shop/[...slug]` will catch `/shop/a`, `/shop/a/b/c` - catch all
- `shop/[[...slug]]` will catch `/shop`, `/shop/a`, `/shop/a/basa/x` - optional catch all

# Route Handlers
describing a special `route.ts` file (in any directory based route),
Allows for multiple HTTP methods to be handled through same route like in an API.
- This can be done by defining `GET`, `POST`, `PUT` etc methods in above file
- the above methods may accept a JS HTTP `Request` object and return a `Response` object
- `NextRequest` and `NextResponse` objects may also be used
- calling third party APIs or URLs from backend may help bypass CORS limitations when calling from browser

## Static vs Dynamic
- when a GET handler doesn't accept any params, it's response is static & can be cached easily
- when a GET handler receives params, its dynamics, any other HTTP method handlers are dynamic by default

## Some Rules
- Route handlers **must be exported as async**
- there **can't** be a `page.js` and a `route.js` in **same directory level**
  - use `app/page.js` & `app/api/route.js`