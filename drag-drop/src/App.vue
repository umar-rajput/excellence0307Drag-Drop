<template>
  <div id="app">
    <!-- <img alt="Vue logo" src="./assets/logo.png" />
    <HelloWorld msg="Welcome to Your Vue.js App" /> -->
    <NodeTree />
    <!-- <TestC></TestC> -->
  </div>
</template>

<script>
// import HelloWorld from "./components/HelloWorld.vue";
import NodeTree from "./components/NodeTree.vue";
// import TestC from "./components/TestC.vue";

export default {
  name: "App",
  components: {
    // HelloWorld,
    NodeTree,
    // TestC,
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
