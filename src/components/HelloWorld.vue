<script setup>

defineProps({
  msg: String
})

</script>

<template>
  <div>
    <h1>{{ msg }}</h1>

    <p>
      Recommended IDE setup:
      <a href="https://code.visualstudio.com/" target="_blank">VSCode</a>
    </p>

    <p>
      <a href="https://vitejs.dev/guide/features.html" target="_blank">
        Vite Documentation
      </a>
      |
      <a href="https://v2.vuejs.org/" target="_blank">Vue 2 Documentation</a>
    </p>

    <p>
      Check
      <code>components/VirtualList.vue</code> to for the source code of infinite list.
    </p>
  </div>
</template>

<style scoped>
a {
  color: #42b983;
}
</style>
