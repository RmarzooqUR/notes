# Intro
- composition vs options api
- can be embedded as standalone widget and for SPAs
- vue template, component and styles
  - template - document structure
  - component - data handling

# SFC
or Single File Components is the standard way of writing components in `.vue` files

An SFC consists of 
- component - for data handling - using options/composition api. `method_name()` method would be defined here
- template - presentation structure of the component
```html
<template>
  <button @click='method_name' class='count_btn'>
    Count: {{ count }}
  </button>
</template>
```
- styles - styles for that component

*Note SFC is not required when using vue as standalone script(like jquery)/ embedding components*

# Options vs Composition API
these are 2 ways vue components can be created
## Options
Exposes predefined methods to handle state, effects etc
example - `data(), methods(), mounted()`

written as - 
```js
export default {
  data(){ //state
    return { count: 0}
  },
  methods: {increment() { this.count++ }, decrement() {this.count--}},  // mutate state
  mounted() { //lifecycle method
    console.log('inital value', this.count)
  }
}
```

## Composition
We can import items & use top level variables directly in templates
written as - 
```html
<script setup>
  import {ref, onMounted} from 'vue'

  const count = ref(0) //state
  const increment = () => count++ //mutate state, no use of this
  onMounted(()=> console.log('init val', count))  // lifecycle method
</script>
```