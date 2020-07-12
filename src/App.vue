<template>
  <div id="app">
    <h1>製麺用分量計算機</h1>
    <div style="display: flex; justify-content: center;">
      <FlourCalculator />
      <TotalCalculator />
    </div>
  </div>
</template>

<script lang="ts">
import { reactive, computed } from "vue";
import FlourCalculator from "@/components/FlourCalculator.vue";
import TotalCalculator from "@/components/TotalCalculator.vue";

export default {
  components: {
    FlourCalculator,
    TotalCalculator
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
  text-align: center;
  margin: 60px 16px;
}
</style>
