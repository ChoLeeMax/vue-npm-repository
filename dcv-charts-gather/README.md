## 工程介绍

修改 package 配置文件组件名称(name)、描述(description)、版本(version)、入口文件（main）；

修改组件目录下的 vue 布局文件，调整为实际组件布局；

修改组件目录下的 js 脚本文件，调整为实际组件实现逻辑；

修改组件目录下的 scss 样式文件，调整为实际组件样式内容；

将组件所需的资源文件放在组件目录下的 assets 文件夹下，注意引用路径；

修改根目录下的组件测试入口文件 index.vue，调整为实际组件调用方式；

修改根目录下的工程配置文件,调整组件名称(name)、描述(description)、版本(version)、入口文件（main）字段；

## 发布组件
在组件dcv-charts-gather目录执行
```js
npm publish
```

## 组件使用

- 安装组件

```js
    npm i dcv-charts-gather
```

- 使用组件

```
<template>
  <div class="chart-gather">
    <div class="module">
      <!-- 使用组件 -->
      <dcvChartsGather
        ref="charts"
        class="ass"
        @chartClick="chartClick"
        :configuration="testData.configuration"
        :information="testData.information"
      ></dcvChartsGather>
    </div>
  </div>
</template>

<script>
// 使用 npm i dcv-charts-gather 命令安装引用
// import dcvChartsGather from 'dcv-charts-gather';
//绝对路径引用，需拷贝组件文佳至本地
// import dcvChartsGather from "./dcv-charts-gather/widge/index.js";
/**
 * @author lichao
 * @version 1.0.0
 * @description 组件使用和测试
 */
export default {
  name: "App",
  // 注册组件
  components: { dcvChartsGather },
  data() {
    return {
      testData: {
        //饼图配置信息
        configuration: {
          // color: ["red"],
          legend: {
            show: false,
            data: ["散点图数据分析"],
            icon: "rect",
          },
          tooltip: {
            show: false,
          },
        },
        information: {
          data: [
            {
              name: "小学",
              type: "",
              total: "",
              unit: "",
              children: [
                {
                  name: "0-10",
                  value: "200",
                  x: "10",
                  y: "2",
                },
                {
                  name: "10-20",
                  value: "155",
                  x: "0",
                  y: "3",
                },
                {
                  name: "20-30",
                  value: "150",
                  x: "6",
                  y: "7",
                },
                {
                  name: "30-40",
                  value: "212",
                  x: "10",
                  y: "0",
                },
                {
                  name: "40-50",
                  value: "420",
                  x: "0",
                  y: "10",
                },
                {
                  name: "50-60",
                  value: "240",
                  x: "5",
                  y: "6",
                },
                {
                  name: "60以上",
                  value: "100",
                  x: "6",
                  y: "9",
                },
              ],
            },
            {
              name: "初中",
              type: "",
              total: "",
              unit: "",
              children: [
                {
                  name: "0-10",
                  value: "200",
                  x: "10",
                  y: "6",
                },
                {
                  name: "10-20",
                  value: "155",
                  x: "6",
                  y: "3",
                },
                {
                  name: "40-50",
                  value: "420",
                  x: "5",
                  y: "10",
                },
                {
                  name: "50-60",
                  value: "240",
                  x: "5",
                  y: "4",
                },
                {
                  name: "60以上",
                  value: "100",
                  x: "7",
                  y: "9",
                },
              ],
            },
            {
              name: "高中",
              type: "",
              total: "",
              unit: "",
              children: [
                {
                  name: "0-10",
                  value: "200",
                  x: "9",
                  y: "2",
                },
                {
                  name: "10-20",
                  value: "155",
                  x: "1",
                  y: "3",
                },
                {
                  name: "20-30",
                  value: "150",
                  x: "6",
                  y: "4",
                },
                {
                  name: "30-40",
                  value: "212",
                  x: "7",
                  y: "3",
                },
              ],
            },
          ],
        },
      },
    };
  },

  mounted() {
    this.$refs.charts.update();
  },
  methods: {
    chartClick(data) {
      // console.log(data);
    },
  },
};
</script>
<style scope lang="scss">
.chart-gather {
  display: flex;
  flex-wrap: wrap;
  .module {
    width: 500px;
    height: 300px;
    border: 1px solid #ccc;
    margin: 12px;
    // padding: 24px;
    background: #011840;
  }
}
</style>

```
