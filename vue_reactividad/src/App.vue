<script setup>
import ref_example from './components/ref_example.vue';
import reactive_example from './components/reactive_example.vue';
import watch_exxample from './components/watch_exxample.vue';
import computed_example from './components/computed_example.vue';
</script>

<template>
  <ref_example />
  <reactive_example />
  <watch_exxample />
  <computed_example />
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
