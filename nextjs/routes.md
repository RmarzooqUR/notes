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
