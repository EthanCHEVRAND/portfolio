<script setup>
import { RouterLink, RouterView } from 'vue-router'
import ArcadeShell from './layout/ArcadeShell.vue'
import router from './router';
</script>

<template>
  <arcade-shell />
</template>

<style>
body {
  margin: 0;
  font-family: 'Press Start 2P', monospace;
  background: radial-gradient(circle at center, #111, #000);
  color: #00ffcc;
}
</style>
