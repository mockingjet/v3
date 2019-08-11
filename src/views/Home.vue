<template>
  <div>
    <svg class="line" width="1000" height="600">
      <path fill="none" stroke="grey" stroke-width="5" />
    </svg>
    <!-- <svg class="bar" width="1000" height="600" /> -->
  </div>
</template>

<script>
import { line as d3Line } from "d3-shape";
import { select } from "d3-selection";
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
    drawLine() {
      let $line = d3Line()
        .x((d, i) => i)
        .y(d => d);
      let line = select("svg.line path");
      line.attr("d", $line(this.chartData));
    },
    drawBar() {
      let bars = select("svg.bar")
        .selectAll(".bars")
        .data(this.chartData);
      // ENTER
      bars
        .enter()
        .append("rect")
        .attr("class", "bars")
        .style("fill", "steelblue")
        .attr("x", (d, i) => i)
        .attr("width", 1)
        .attr("y", 0)
        .attr("height", d => d);

      // UPDATE
      bars
        .style("fill", "steelblue")
        .attr("x", (d, i) => i)
        .attr("width", 1)
        .attr("y", 0)
        .attr("height", d => d);

      // EXIT
      bars.exit().remove();
    }
  },
  watch: {
    chartData() {
      this.drawLine();
      this.drawBar();
    }
  }
};
</script>

<style lang="scss" scoped>
</style>