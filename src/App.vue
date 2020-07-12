<template>
  <div id="app">
    <h1>製麺用分量計算機</h1>
    <h2>
      茹で前
      <input type="number" min="0" max="10000" size="8" v-model="state.amountTotal" />g 作る
    </h2>
    <table>
      <tbody>
        <tr>
          <th>材料</th>
          <th>割合</th>
          <th>分量</th>
        </tr>
        <tr>
          <td>小麦粉</td>
          <td></td>
          <td class="amount">{{state.amountFlour.toFixed()}}g</td>
        </tr>
        <tr>
          <td>水</td>
          <td>
            <input type="number" min="0" max="100" size="4" v-model="state.rateWater" />%
          </td>
          <td class="amount">{{state.amountWater.toFixed()}}ml</td>
        </tr>
        <tr>
          <td>塩</td>
          <td>
            <input type="number" min="0" max="100" size="4" v-model="state.rateSalt" />%
          </td>
          <td class="amount">{{state.amountSalt.toFixed(1)}}g</td>
        </tr>
        <tr>
          <td>粉末かんすい</td>
          <td>
            <input type="number" min="0" max="100" size="4" v-model="state.rateIyeWater" />%
          </td>
          <td class="amount">{{state.amountIyeWater.toFixed(1)}}g</td>
        </tr>
        <tr>
          <td>全卵</td>
          <td>
            <input type="number" min="0" max="100" size="4" v-model="state.rateEgg" />%
          </td>
          <td>{{state.amountEgg.toFixed(1)}}g</td>
        </tr>
      </tbody>
    </table>
    <button @click="increment">Count is: {{ state.count }}, double is: {{ state.double }}</button>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import { reactive, computed } from "vue";

export default {
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

h1 {
  text-align: center;
}

td {
  padding: 4px 16px;
}

.amount {
  text-align: right;
}
</style>
