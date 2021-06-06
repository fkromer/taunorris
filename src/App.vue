<template>
  <Header />
  <br />
  <JokeRequest />
</template>

<script lang="ts">
import { defineComponent } from "vue";
import JokeRequest from "./components/JokeRequest.vue";
import Header from "./components/Header.vue";

export default defineComponent({
  name: "App",
  components: {
    Header,
    JokeRequest,
  },
});
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
