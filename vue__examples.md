# Example Vue Files

## Standard main.js for Vue

~~~javascript
import Vue from 'vue'
import App from './App'

new Vue({
  render: h => h(App)
}).$mount('#app')
~~~

## Standard App.vue component

    
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

## Standard SubComponent

    <template>
      <div>
        <input @input="onInput" />
      </div>
    </template>

    <script>
    export default {
      methods: {
        onInput: function(event) {
          console.log(event.target.value)
        }
      }
    }
    </script>

    <style>

    </style>
