<template>
  <div id="app">
    <home></home>
  </div>
</template>

<script>
import Home from "@/views/Home.vue";

export default {
  name: "App",
  methods: {},
  components: { Home }
};
</script>

<style scoped>
</style>

<style>
html {
  margin: 0;
  padding: 0;
}
body {
  margin: 0;
  padding: 0;
  font-size: 16px;
  font-family: "Open Sans", sans-serif;
  color: #232321;
  background: #fff !important;
}
html,
body,
#app {
  height: 100%;
  width: 100%;
  box-sizing: border-box;
  background-color: rgb(31, 39, 57);
}
#app {
  overflow: auto;
}

* {
  margin: 0;
  padding: 0;
}
</style>