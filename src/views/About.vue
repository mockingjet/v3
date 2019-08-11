<template>
  <div>
    <svg width="1000" height="600">
      <path :d="pathData" fill="none" stroke="grey" stroke-width="5" />
    </svg>
    <!-- <svg width="1000" height="600">
      <rect
        v-for="(data,i) in chartData"
        style="fill:grey"
        :key="i"
        :x="i"
        y="0"
        width="1"
        :height="data"
      />
    </svg>-->
  </div>
</template>

<script>
import { line as d3Line } from "d3-shape";
export default {
  data() {
    return {
      chartData: [...Array(500)].map(() => Math.random() * 1000)
    };
  },
  mounted() {
    setInterval(() => {
      // this.chartData = [...Array(500)].map(() => Math.random() * 1000);
      this.chartData.push(Math.random() * 1000);
    }, 100);
  },
  methods: {
    createLine() {
      return d3Line()
        .x((d, i) => i)
        .y(d => d);
    }
  },
  computed: {
    pathData() {
      return this.createLine()(this.chartData);
    }
  }
};
</script>

<style lang="scss" scoped>
</style>