<template>
  <div id="app">
    <Pomodoro/>
    <Todolist/>
  </div>
</template>

<script>

import Todolist from './components/todolist.vue'
import Pomodoro from './components/pomodoro.vue'
import './styles/global.css'


export default {
  name: 'App',
  components: {
    Pomodoro,
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
  margin-top: 20px;
}
</style>
