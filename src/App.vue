<script setup>

import HelloWorld from './components/HelloWorld.vue'

// `VirtualList` is a prototype showing how to implement an infinite list in vue
import VirtualList from './components/VirtualList.vue'
</script>

<template>
  <div>
    <img width="100" alt="Vue logo" src="./assets/logo.png" />
    <HelloWorld msg="Demo built on `Vue2` with the build tool of `Vite`" />
    <VirtualList />
  </div>
</template>

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
