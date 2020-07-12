<template>
  <div class="calculator">
    <h2>
      茹で
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
          <td class="amount">{{state.amountEgg.toFixed(1)}}g</td>
        </tr>
      </tbody>
    </table>
    <p>
      <a href="https://twitter.com/intent/tweet?text=Hello%20world">ツイートして自慢する</a>
    </p>
  </div>
</template>

<script lang="ts">
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
      shareText: computed(() => (state.amountFlour * state.rateEgg) / 100)
    });

    return {
      state
    };
  }
};
</script>

<style>
h1 {
  text-align: center;
}

td {
  padding: 4px 16px;
}

.calculator {
  border: 1px solid #ccc;
  border-radius: 8px;
  padding: 16px;
}

.amount {
  text-align: right;
}
</style>
