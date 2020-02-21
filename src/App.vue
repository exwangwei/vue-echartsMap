<template>
  <div id="app">
    <div id="myEchart" ref="myEchart" :style="{height:'800px',width:'100%'}"></div>
  </div>
</template>

<script>
import echarts from "echarts";
import "./../node_modules/echarts/map/js/china.js";
export default {
  data() {
    return {
      myData: [
        { name: "海门", value: [121.15, 31.89, 60] },
        { name: "鄂尔多斯", value: [109.781327, 39.608266, 180] },
        { name: "招远", value: [120.38, 37.35, 300] },
        { name: "舟山", value: [122.207216, 29.985295, 20] }
      ]
    };
  },
  mounted() {
    this.chinaConfigure();
  },
  methods: {
    chinaConfigure() {
      var that = this;
      let myChart = echarts.init(this.$refs.myEchart); //这里是为了获得容器所在位置
      window.onresize = myChart.resize;
      myChart.setOption({
        // 进行相关配置
        backgroundColor: "#02AFDB",
        geo: {
          // 这个是重点配置区
          map: "china", // 表示中国地图
          roam: true,
          label: {
            normal: {
              show: true // 是否显示对应地名
            }
          },
          itemStyle: {
            // 定义样式
            normal: {
              // 普通状态下的样式
              areaColor: "#323c48",
              borderColor: "#111"
            },
            emphasis: {
              // 高亮状态下的样式
              areaColor: "#2a333d"
            }
          }
        },
        series: [
          {
            name: "销量",
            type: "scatter",
            coordinateSystem: "geo", // 对应上方配置
            symbolSize: function(data) {
              console.log("data", data);
              return data[2] / 10;
            },

            data: that.myData
          }
        ]
      });
    }
  }
};
</script>

<style>
</style>
