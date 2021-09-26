<template>
  <div>
    <div v-if="totalAmount && totalInterest">
      <GChart type="PieChart" :options="options" :data="graphData" />
    </div>
    <div v-else>
      Graph Data 0%
    </div>
  </div>
</template>

<script>
import { GChart } from "vue-google-charts";

export default {
  name: "App",
  props: ["totalAmount", "totalInterest"],
  components: {
    GChart,
  },
  data() {
    return {
      options: {
        width: 550,
        height: 300,
      },
    };
  },
  computed: {
    graphData() {
      return [
        ["Total Breakupable Amount", "Percentage"],
        [
          "Interest",
          this.totalInterest && this.totalAmount
            ? (this.totalInterest * 100) / this.totalAmount
            : 0,
        ],
        [
          "Payable Amount",
          this.totalInterest && this.totalAmount
            ? 100 - (this.totalInterest * 100) / this.totalAmount
            : 0,
        ],
      ];
    },
  },
};
</script>
