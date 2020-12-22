<template>
  <div id="app">
    <!-- <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <screenshot></screenshot>
  </div>
</template>

<script>
//import HelloWorld from './components/HelloWorld.vue'
import screenshot from "./components/screenshot.vue";

export default {
  name: "App",
  components: {
    //HelloWorld,
    screenshot,
  },
};
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
