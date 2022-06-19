<template>
  <div class="hello">
    <h3 v-bind:class="counter! % 2 === 0 ? 'even' : 'odd'">
      count: {{ counter }}
    </h3>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  name: "HelloWorld",
  props: {
    msg: String,
    counter: Number,
  },
});
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
h3.even {
  color: #42b983;
}
h3.odd {
  color: #8a2be2;
}
</style>
