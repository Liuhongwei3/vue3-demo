<template>
  <img alt="Vue logo" src="./assets/logo.png" />
  <!-- <Reactive /> -->
  <!-- <Ref/> -->
  <Array/>
  <Object />
</template>

<script>
import Reactive from "./components/Reactive.vue";
import Ref from "./components/Ref";
import Array from "./components/Array";
import Object from "./components/Object";

export default {
  name: "App",
  components: {
    Reactive,
    Ref,
    Array,
    Object,
  },
};
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
