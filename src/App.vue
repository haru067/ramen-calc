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
    const state = reactive({
      rateWater: 35,
      rateSalt: 1,
      rateIyeWater: 1,
      rateEgg: 0,
      amountTotal: 0,
      amountFlour: computed(
        () =>
          (100 * state.amountTotal) /
          (100.0 +
            state.rateWater +
            state.rateEgg +
            state.rateSalt +
            state.rateIyeWater)
      ),
      amountWater: computed(() => (state.amountFlour * state.rateWater) / 100),
      amountSalt: computed(() => (state.amountFlour * state.rateSalt) / 100),
      amountIyeWater: computed(
        () => (state.amountFlour * state.rateIyeWater) / 100
      ),
      amountEgg: computed(() => (state.amountFlour * state.rateEgg) / 100),
      shareText: computed(() => (state.amountFlour * state.rateEgg) / 100),
    });

    function increment() {
      state.count++;
    }

    return {
      state,
      increment
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
