## 工程介绍

修改 package 配置文件组件名称(name)、描述(description)、版本(version)、入口文件（main）；

修改组件目录下的 vue 布局文件，调整为实际组件布局；

修改组件目录下的 js 脚本文件，调整为实际组件实现逻辑；

修改组件目录下的 scss 样式文件，调整为实际组件样式内容；

将组件所需的资源文件放在组件目录下的 assets 文件夹下，注意引用路径；

修改根目录下的组件测试入口文件 index.vue，调整为实际组件调用方式；

修改根目录下的工程配置文件,调整组件名称(name)、描述(description)、版本(version)、入口文件（main）字段；

## 组件截图

![image](https://github.com/ChoLeeMax/vue-npm-repository/blob/master/images/pie.jpg)

## 发布组件
在组件dcv-charts-pie目录执行
```js
npm publish
```

## 组件使用

- 安装组件

```js
    npm i dcv-charts-pie
```

- 使用组件

```
<template>
  <div class="pie-chart">
    <!-- 使用组件 -->
    <pieChart ref="charts" class="ass" @chartClick="chartClick" :information="information"></pieChart>
  </div>
</template>

<script>

// 使用 npm i dcv-charts-pie 命令安装引用
// import pieChart from 'dcv-charts-pie';
//绝对路径引用，需拷贝组件文佳至本地
// import pieChart from "./dcv-charts-pie/widge/index.js";

/**
 * @author lichao
 * @version 1.0.0
 * @description 组件使用和测试
 */
//图例朝向
const rightVertical = {
  unit: "条",//图例名称单位
  hidden: "true",//时候只显示图例名称
  orient: "vertical",
  right: "24px", //距离容器右侧边距
  y: "middle" //竖向y轴居中
};
const topHorizontal = {
  orient: "horizontal",
  top: "0" //距离容易顶部边距
};

export default {
  name: "App",
  // 注册组件
  components: { pieChart },
  data() {
    return {
      //饼图配置信息
      information: {
        position: {
          // radius : '75%',//实心饼图,
          radius: ["45%", "70%"], //空心饼图
          center: ["30%", "50%"], //饼图中心点默认值
          split: 0 //饼图分割价格
        },
        chatStyle: {
          name: "数据来源分析", //饼图名称，如事件类型
          color: ["#4150D8", "#28BF7E", "#F2A93B", "#F9CF36", "#FFEC00"], //渲染颜色
          legend: rightVertical, //默认向右竖向排列,topHorizontal顶部水平排列
          label: {
            normal: {
              show: true, //false不显示
              verticalAlign: "middle",
              position: "center", //outside饼图外,center饼图内
              // formatter:"{c}",//模板变量有{a}、{b}、{c}，分别表示系列名，数据名，数据值。
              // formatter: "{normal|" + "2018年" + "}", //格式1:一行文字
              formatter: ["{big|222}", "{default|数据总量}"].join("\n"), //格式2:二行文字
              // formatter:['{normal|'+"截止"+'}','{normal|'+"2018年"+'}','{normal|'+"8月"+'}'].join('\n'),//格式3:三行文字
              // formatter:['{bold|'+"2358"+'}','{small|'+"wifi热点数量(个)"+'}'].join('\n'),//格式4:二行文字,不同样式
              rich: {
                //label样式
                default: {
                  //用于时间、地点描述
                  fontSize: 18,
                  // fontWeight: 400,
                  padding: [5, 0],
                  fontFamily: "PingFangSC-Regular,PingFangSC",
                  color: "#333333",
                  align: "center"
                },
                big: {
                  //用于总数描述
                  fontSize: 24,
                  fontWeight: "bold",
                  fontFamily: "PingFangSC-Regular,PingFangSC",
                  color: "#333333",
                  lineHeight: 42,
                  align: "center"
                }
              }
            }
          }
        },
        data: []
      }
    };
  },
  methods: {
    /**
     * 饼图点击回调事件
     */
    chartClick(data) {
      console.log(data);
    }
  },
  mounted() {
    this.information.data = [];
    const data = [
      { value: 35, name: "小汽车" },
      { value: 310, name: "小轿车" },
      { value: 4, name: "宇宙飞船" },
      { value: 135, name: "飞机大炮" }
    ];
    this.information.data = data;
    this.$refs.charts.update(this.information);
    this.$refs.charts.responseChart();
  }
};
</script>
<style lang="scss" scoped>
.pie-chart {
  height: 250px;
  width: 400px;
  border: solid 1px #999999;
}
</style>

```
