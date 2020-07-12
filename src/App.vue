<template>
  <div id="app">
    <h1>製麺用分量計算機</h1>
    <FlourCalculator />
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import { reactive, computed } from "vue";
import FlourCalculator from "@/components/FlourCalculator.vue";

export default {
  components: {
    FlourCalculator
  },
  setup() {
    const state = reactive({});

    return {
      state
    };
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin: 60px 16px;
}
</style>
