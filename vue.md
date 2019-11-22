# Vue.js

<img src="https://vuejs.org/images/logo.png" width=128px>

## Standard main.js for Vue

```javascript
import Vue from 'vue'
import App from './App'

new Vue({
  render: h => h(App)
}).$mount('#app')
```

## Standard App.vue component

```xml
<template>
  <div>
    <SearchBar></SearchBar>
  </div>
</template>

<script>
import SearchBar from './components/SearchBar';

export default {
  name: "App",
  components:{
    SearchBar
  }
}
</script>

<style>
</style>
```

## Standard SubComponent

```xml
<template>
  <div>
    <input @input="onInput" />
  </div>
</template>

<script>
export default {
  methods: {
    onInput: function(event) {
      /* eslint-disable  no-console */
      console.log(event.target.value)
      /* eslint-enable  no-console */
    }
  }
}
</script>

<style>

</style>
```

[Back to Index](index.md)
