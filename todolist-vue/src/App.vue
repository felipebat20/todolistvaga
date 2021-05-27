<template>
  <div id="app">
    <Todolist/>
  </div>
</template>

<script>

import Todolist from './components/todolist.vue'
import './styles/global.css'


export default {
  name: 'App',
  components: {
    Todolist
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
