<template>
  <div class="app">
    <Navbar />
    <RouterView></RouterView>
  </div>
</template>

<script>
import Navbar from "@/components/Navbar.vue";

export default {
  components: {Navbar}
}
</script>

<style>
* {
  font-family: "Inter", sans-serif;
  box-sizing: border-box;
  color: #3B4256;
  padding: 0;
  margin: 0;
}
body {
  background-color: #E7F2FD;
}
.app {
  background-color: #fff;
  max-width: 1000px;
  min-height: 100vh;
  height: 100%;
  padding: 20px;
  margin: 0 auto;
}
.highlight {
  background-color: #FFEA8A;
}
</style>