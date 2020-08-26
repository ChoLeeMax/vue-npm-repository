<template>
  <div class="dcv-chart-gather-main">
    <div class="chart-gather-main" ref="dcvChartsGather"></div>
  </div>
</template>

<script>
/**
 * @author lichao
 * @version 1.0.0  2020-6-8 组件初始化开发
 * @version 1.0.1  2020-6-10 组件x、y轴重新配置
 * @version 1.0.2  2020-6-11 组件输入数据格式化(大屏数据格式4)
 *
 * @description 散点图
 *
 * @memo 使用说明
 */
// 引用文件
import "./js/index";
// 主题颜色
export default {
  name: "dcvChartsGather",
  props: {
    // 样式/配置
    configuration: {
      type: Object,
      default: () => {
        return {};
      }
    },
    // 数据
    information: {
      type: Object,
      default: () => {
        return {};
      }
    },
    // 局部主题
    theme: {
      type: String,
      default: () => {
        return "";
      }
    }
  },
  data() {
    return {
      myChart: null,
    };
  },
  watch: {
    /**
     * 更新局部主题
     * @param {String} 局部主题名称 theme
     */
    information(val) {
      this.update(val);
    }
  },
  created() {
  },
  methods: {
    update(information) {
      console.log(information)
      const configuration = this.configuration;
      let seriesName = configuration.legend ? configuration.legend.data[0] : "";
      let _information = information || this.information;
      let datas = _information.data;
      let yAxisData = [];
      let xAxisData = [];
      let seriesData = [];
      datas.forEach((item, index) => {
        yAxisData.push(item.name);
        item.children.forEach(child => {
          if (index == 0) {
            xAxisData.push(child.name);
          }
          seriesData.push([
            parseFloat(child.x),
            parseFloat(child.y),
            child.value,
            child.name,
            item.name
          ]);
        });
      });
      let option = {
        color: configuration.color?configuration.color:["red"],
        textStyle: {
          color: "#597CAA"
        },
        tooltip: Object.assign(
          {
            trigger: "axis",
            show: true,
            formatter: function(params) {
              let str = "";
              params.forEach(item => {
                str +=
                  item.marker +
                  item.value[4] +
                  item.value[3] +
                  "：" +
                  item.value[2] +
                  "<br>";
              });
              return str;
            },
            axisPointer: {
              type: "line",
              show: true,
              lineStyle: {
                type: "solid",
                width: 2,
                color: "#4B941A"
              },
              animation: true
            }
          },
          configuration.tooltip
        ),
        legend: Object.assign(
          {
            show: false,
            left: "center",
            top: "3%",
            textStyle: {
              color: "#597CAA"
            },
            icon: "rect",
            itemWidth: 24,
            itemHeight: 8
          },
          configuration.legend
        ),
        grid: {
          show: false
        },
        yAxis: [
          {
            type: "value",
            show: false
          },
          {
            type: "category",
            position: "left",
            data: yAxisData,
            axisLine: {
              show: false
            },
            axisTick: {
              show: false
            },
            splitLine: {
              show: false
            },
            axisLabel: {
              fontSize: 12
            }
          }
        ],
        xAxis: [
          {
            type: "value",
            show: false
          },
          {
            data: xAxisData,
            type: "category",
            position: "bottom",
            boundaryGap: false,
            splitLine: {
              show: true,
              lineStyle: {
                color: "#526FA5",
                type: "solid"
              }
            },
            axisLine: {
              show: false
            },
            axisTick: {
              show: false
            },
            axisLabel: {
              fontSize: 12
            }
          }
        ],
        series: {
          name: seriesName,
          type: "scatter",
          symbol: "circle",
          symbolSize: function(data) {
            return Math.sqrt(data[2]) * 1;
          },
          itemStyle: {
            normal: {
            }
          },
          data: seriesData
        }
      };
      if (this.myChart) this.myChart.clear();
      this.myChart = this.$echarts.init(this.$refs.dcvChartsGather);
      this.myChart.setOption(option);
      //点击事件交互
      let that = this;
      this.myChart.on("click", function(params) {
        that.$emit("chartClick", params);
      });
    },
    responseChart() {
      if (this.myChart) {
        this.myChart.resize();
      } else {
        this.myChart = this.$echarts.init(this.$refs.dcvChartsGather);
      }
    }
  }
};
</script>

<style lang="scss">
@import "./style/index.scss";
.dcv-chart-gather-main {
  width: 100%;
  height: 100%;
  position: relative;
  .chart-gather-main {
    width: 100%;
    height: 100%;
  }
}
</style>
