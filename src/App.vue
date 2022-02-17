<template>
  <v-app id="app">
    <router-view />
    <Footer></Footer>
  </v-app>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>

<script>
import Footer from "./components/Footer.vue";
export default {
  components: {
    Footer,
  },
};
</script>
