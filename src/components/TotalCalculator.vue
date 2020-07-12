<template>
  <div class="calculator">
    <h2>
      合計
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
      <a v-bind:href="state.shareText">ツイートして自慢する</a>
    </p>
  </div>
</template>

<script lang="ts">
import { reactive, computed } from "vue";

export default {
  setup() {
    function getShareText(state) {
      let eggText = "";
      if (state.amountEgg > 0) {
        eggText = `, 卵 ${state.amountEgg}g`;
      }
      return `小麦粉 ${state.amountFlour}g, 水 ${state.amountWater}ml, 塩 ${state.amountSalt}g, かんすい ${state.amountIyeWater}g${eggText} ${window.location.href}`;
    }   

    const state = reactive({
      rateWater: 35,
      rateSalt: 1,
      rateIyeWater: 1,
      rateEgg: 0,
      amountTotal: 500,
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
      shareText: computed(() => "https://twitter.com/intent/tweet?text=" + getShareText(state))
    });

    return {
      state
    };
  }
};
</script>

<style scoped>
table {
  margin: 32px;
}

th {
  text-align: center;
  padding: 4px 16px;
}

td {
  padding: 4px 16px;
}

h2 {
  text-align: center;
}

p {
  text-align: center;
}

div.calculator {
  border: 1px solid #ccc;
  border-radius: 8px;
  margin: 0px 32px;
  padding: 16px;
  text-align: left;
}

td.amount,
th.amount {
  text-align: right;
}
</style>
