<template>
  <multi-image-uploader />
</template>

<script>
import MultiImageUploader from './components/multi-image-uploader.vue'

export default {
  name: 'App',
  components: {
    MultiImageUploader
  }
}
</script>

<style>
/* RESET */
*,
*::before,
*::after {
  box-sizing: border-box;
}
body {
  width: 100vw;
  height: 100vh;
  display: grid;
  place-items: center;
  margin:0;
  font-family: system-ui;
}
</style>
