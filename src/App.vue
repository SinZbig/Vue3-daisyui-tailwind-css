<template>
  <navbar />
  <div class="m-14">
    <router-view />
  </div>
</template>
<script setup>
import navbar from './components/navbar.vue'
import content from './views/content.vue'
</script>
<style lang="scss" scoped>
  
</style>
