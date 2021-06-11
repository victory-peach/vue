<template>
  <div class="echarts-content">
    <div :id="id" />
  </div>
</template>

<script>
import * as echarts from "echarts";
export default {
  props: ["layout","coltarget"],
  data() {
    return {
      chart: null,
      id: "main",
      option: null,
      allArr: {},
    };
  },
  mounted() {
    this.initChart();
  },
  beforeDestroy() {
    if (!this.chart) {
      return;
    }
    this.chart.dispose();
    this.chart = null;
  },
  methods: {
    initChart() {
      this.chart = echarts.init(document.getElementById(this.id));
      this.option = {
        animation: false,
        // grid: {
        //   top: 40,
        //   left: 50,
        //   right: 40,
        //   bottom: 50,
        // },
        xAxis: {
          name: "x",
          minorTick: {
            show: true,
          },
          minorSplitLine: {
            show: true,
          },
        },
        legend: {
          data: ["default"],
        },
        yAxis: {
          name: "y",
          min: -100,
          max: 100,
          minorTick: {
            show: true,
          },
          minorSplitLine: {
            show: true,
          },
        },
        dataZoom: [
          {
            show: true,
            type: "inside",
            filterMode: "none",
            xAxisIndex: [0],
            startValue: -20,
            endValue: 20,
          },
          {
            show: true,
            type: "inside",
            filterMode: "none",
            yAxisIndex: [0],
            startValue: -20,
            endValue: 20,
          },
        ],
        series: [
          {
            type: "line",
            name: "default",
            showSymbol: false,
            clip: true,
            data: this.generateData(), // 第一列对应 X 轴，第二列对应 Y 轴。
          },
        ],
        tooltip: {
          trigger: "none",
          axisPointer: {
            type: "cross",
          },
        },
      };
      this.option && this.chart.setOption(this.option);
    },
    someFunc() {
      if (this.layout) {
        if (this.option.series.length != 0) {
          this.option.series.splice(1, this.option.series.length - 1);
        }
        for (const key in this.layout) {
          if (this.layout[key]) {
            this.option.legend.data.push(`line${key}`);
            this.option.series.push({
              type: "line",
              showSymbol: false,
              clip: true,
              data: this.allArr[key],
              name: `line${key}`,
            });
          }
        }
      }
      this.chart.setOption(this.option);
    },
    func(item, x) {
      if (this.layout) {
        if (item && typeof item == "string") {
          return new Function(`return ${item.replace(/x/g, `${x}`)}`);
        }
      }
      if(this.coltarget){
        // console.log('jdhsj');
      return new Function(`return ${this.coltarget.replace(/x/g, `${x}`)}`);

      }
      return new Function(`return Math.sin(${x})`);

    },
    generateData() {
      if (this.layout) {
        for (const key in this.layout) {
          let data = [];
          if (Object.hasOwnProperty.call(this.layout, key)) {
            const element = this.layout[key];
            // console.log(element);
            for (let j = -10; j <= 10; j += 0.1) {
              data.push([j, this.func(element, j)()]);
            }
            this.allArr[key] = data;
          }
          this.someFunc();
        }
        // return;
      }
      let data = [];
      for (let i = -10; i <= 10; i += 0.1) {
        data.push([i, this.func(0, i)()]);
      }
      if (this.option) {
        this.chart.setOption(this.option);
      }
      return data;
    },
  },
  watch: {
    layout: {
      handler() {
        clearTimeout(this.timeout);
        this.timeout = setTimeout(() => {
          this.generateData();
          this.chart.setOption(this.option);
        }, 1000);
      },
      deep: true,
    },
    coltarget(){
     this.initChart();
    }
    
  },
};
</script>
<style scoped>
#main {
  width: 100%;
  height: 100%;
}
</style>