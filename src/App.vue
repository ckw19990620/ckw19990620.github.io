<script setup lang="ts">
import FrameAnimation from './components/FrameAnimation.vue'
</script>

<template>
  <FrameAnimation 
    :frame-count="10"
    :frame-height="800"
    :sensitivity="1.2"
  />
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
