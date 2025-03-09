
# Design Patterns
- should know when to use and where to use
- used when you transition from framework consumer to framework creator 

(only list, find details)
+ Singleton Pattern
+ Facade Pattern
+ Bridge/Adapter Pattern
+ Strategy Pattern
+ Observer Pattern(pub/sub)


# Code Quality / Readibility
- **Inversion** of nested if statements
  - nested if statements can be cleaned up by inverting their conditions
```py
if a:
  if b:
    if c:
      return c
  else:
    return b
else:
  return a
```
to
```py
if !a:
  return a
if !b:
  return b
return c
```
- **Extraction** of logic into simple named funtions
- Properly **Naming variables** - (hardest thing)

- When needing to add properties to classes / types / interfaces
  - Extend the original class rather than adding props in the same class
