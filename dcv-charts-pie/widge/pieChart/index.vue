<template>
  <div class="dcv-pie-chart-main">
    <div class="pie-chart-main" ref="pieChartMain"></div>
  </div>
</template>

<script>
/**
 * @author lichao
 * @version 1.0.0
 * @description 饼图
 * @update cholee 20200204增加中间label自定义显示
 * @update cholee 20200327增加饼图交互事件
 * @update 1.2.9 20200402 jjh 优化放大缩小适配
 *
 * @memo 使用说明
 */
// 引用文件
import "./js/index";
export default {
  name: "pieChart",
  props: {
    information: Object
  },
  data() {
    return {
      myChart: null,
      sort: 0,
      rightVertical: {
        orient: "vertical",
        right: 24, //距离容器右侧边距
        y: "middle" //竖向y轴居中
      },
      legendStyle: {
        itemGap: 12, //图例间隔
        icon: "circle",
        // width:100,
        itemWidth: 10, //图例宽
        itemHeight: 10, //图例高
        borderRadius: 10,
        data: null
      }
    };
  },
  watch: {
    information(val) {
      this.update(val);
    }
  },
  methods: {
    update(information) {
      information = information || this.information;
      let _chatStyle = information.chatStyle;
      let legendData = [];
      for (let index = 0; index < information.data.length; index++) {
        const element = information.data[index];
        legendData.push(element.name);
      }
      let legendObj = {};
      if (_chatStyle && _chatStyle.legend) {
        legendObj = _chatStyle.legend;
      } else {
        legendObj = this.rightVertical;
      }
      for (const key in legendObj) {
        if (legendObj.hasOwnProperty(key)) {
          const item = legendObj[key];
          this.legendStyle[key] = item;
        }
      }
      if (!_chatStyle.legend.hidden) {
        let unit = _chatStyle.legend.unit;
        this.legendStyle.formatter = name => {
          var value = 0;
          information.data.map((item, index) => {
            if (item.name === name) {
              if (item.value) {
                value = item.value;
              }
            }
          });
          var str = name + "{b|" + value + "}";
          if (unit) {
            str += unit;
          }
          return str;
        };
        this.legendStyle.textStyle = {
          rich: {
            b: {
              fontFamily: "PingFangSC-Regular,PingFangSC",
              fontSize: 24,
              width: 50,
              align: "right",
              padding: [0, 12, 0, 12],
              color: _chatStyle.color[this.sort]
            }
          }
        };
      }
      let label = { normal: { show: false, formatter: "{c}" } };
      if (_chatStyle && _chatStyle.label) {
        label = Object.assign({}, label, _chatStyle.label);
      }

      let title = {};
      if (_chatStyle && _chatStyle.title) {
        title = _chatStyle.title;
      }

      let option = {
        title: title,
        tooltip: {
          trigger: "item",
          formatter: "{a} <br/>{b} : {c}"
        },
        legend: this.legendStyle,
        series: [
          {
            name: _chatStyle ? _chatStyle.name : " ",
            type: "pie",
            radius: information.position ? information.position.radius : "75%",
            center: information.position
              ? information.position.center
              : ["40%", "50%"],
            label: label,
            itemStyle: {
              borderWidth: information.position
                ? information.position.split
                : 0,
              borderColor: "#FFFFFF",
              emphasis: {
                shadowOffsetX: 0
              }
            },
            lableLine: {
              normal: {
                show: true
              },
              emphasis: {
                show: false
              }
            },
            data: information.data,
            color: _chatStyle ? _chatStyle.color : []
          }
        ]
      };
      this.myChart = this.$echarts.init(this.$refs.pieChartMain);
      this.myChart.setOption(option);
      //点击事件交互
      let that = this;
      this.myChart.on("click", function(params) {
        let data = params.data;
        data.seriesIndex = params.seriesIndex;
        that.$emit("chartClick", data);
      });
    },
    responseChart() {
      if (this.myChart) {
        this.myChart.resize();
      }
    }
  }
};
</script>

<style lang="scss">
@import "./style/index.scss";
.dcv-pie-chart-main {
  width: 100%;
  height: 100%;
  position: relative;
  .pie-chart-main {
    width: 100%;
    height: 100%;
  }
}
</style>
