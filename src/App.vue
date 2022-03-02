<template>
  <div id="app">
    <app-home />
  </div>
</template>
<script>
import appHome from "@/views/Home.vue";
export default {
  components: {
    appHome,
  },
  mounted() {},
};
</script>

<style>
body,
html {
  height: 100%;
}
#app {
  height: 100%;
  width: 100%;
  color: #0c0c0c;
}
</style>
