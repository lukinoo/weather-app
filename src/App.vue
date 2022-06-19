<template>
  <img alt="Vue logo" src="./assets/logo.png" />
  <HelloWorld msg="hello world" :counter="counter" />
  <button v-on:click="increment()">increment</button>
  <button v-on:click="decrement()">decrement</button>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import HelloWorld from "./components/HelloWorld.vue";

export default defineComponent({
  name: "App",
  components: {
    HelloWorld,
  },
  data() {
    return {
      counter: 0,
    };
  },
  methods: {
    increment() {
      this.counter += 1;
    },
    decrement() {
      this.counter -= 1;
    },
  },
});
</script>

<style lang="less">
#app {
}
</style>
