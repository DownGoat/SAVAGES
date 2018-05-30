<template>
  <div id="app">
    <img class="logo" src="./assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'app',
  components: {
    HelloWorld
  }
}
</script>

<style>
body {
  background-color: #1e1e1e;
}
input {
  background-color: #2e2e2e;
  color: #cccccc;
  border: 0;
}
.logo {
  margin-bottom: 3em;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  margin-top: 60px;
  color: #cccccc;
}
</style>
