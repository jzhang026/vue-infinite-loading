<script setup>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup
import HelloWorld from './components/HelloWorld.vue'

// `VirtualList` is a prototype showing how to implement an infinite list in vue
import VirtualList from './components/VirtualList.vue'
</script>

<template>
  <img width="100" alt="Vue logo" src="./assets/logo.png" />
  <HelloWorld msg="Demo built on `Vue3` with the build tool of `Vite`" />
  <VirtualList />
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
