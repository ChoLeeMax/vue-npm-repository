<!--
 * @Descripttion:
 * @version:
 * @Author: cholee
 * @Date: 2020-06-09 16:52:04
 * @LastEditors: cholee
 * @LastEditTime: 2020-08-26 14:20:56
-->

## 工程介绍

修改 package 配置文件组件名称(name)、描述(description)、版本(version)、入口文件（main）；

修改组件目录下的 vue 布局文件，调整为实际组件布局；

修改组件目录下的 js 脚本文件，调整为实际组件实现逻辑；

修改组件目录下的 scss 样式文件，调整为实际组件样式内容；

将组件所需的资源文件放在组件目录下的 assets 文件夹下，注意引用路径；

修改根目录下的组件测试入口文件 index.vue，调整为实际组件调用方式；

修改根目录下的工程配置文件,调整组件名称(name)、描述(description)、版本(version)、入口文件（main）字段；

## 发布组件
在组件dvc-txt-list目录执行
```js
npm publish
```

## 组件使用

- 安装组件

```js
    npm i dvc-txt-list
```

- 使用组件

```
<template>
  <div class="dcv-txt-list">
    <div class="module" data-theme="default-theme">
      <!-- 使用组件 -->
      <dcvtxtlist
        :configuration="testData.configuration"
        :information="testData.information"
        :theme="theme"
      ></dcvtxtlist>
    </div>
  </div>
</template>

<script>
// 使用 npm i dcv-txt-list 命令安装引用
// import dcvtxtlist from 'dcv-txt-list';
//绝对路径引用，需拷贝组件文佳至本地
// import dcvtxtlist from "./dcv-txt-list/widge/index.js";
/**
 * @author lichao
 * @version 1.0.0
 * @description 组件使用和测试
 */
export default {
  name: "App",
  // 注册组件
  components: { dcvtxtlist },
  data() {
    // TODO 初始化数据
    return {
      testData: {
        configuration: {
          fontSize: 16,//列表默认字体
          themeColor: "#2196f3",//列表默认背景颜色
        },
        information: {
          data: [
            {
              name: "序号",
              unit: "",
              children: [
                {
                  name: "",
                  value: "1",
                },
                {
                  name: "",
                  value: "2",
                },
                {
                  name: "",
                  value: "3",
                },
                {
                  name: "",
                  value: "4",
                },
                {
                  name: "",
                  value: "5",
                },
                {
                  name: "",
                  value: "6",
                },
              ],
            },
            {
              name: "区域名称",
              unit: "",
              children: [
                {
                  name: "",
                  value: "抚顺北站",
                },
                {
                  name: "",
                  value: "抚顺职业技术学院",
                },
                {
                  name: "",
                  value: "抚顺北站",
                },
                {
                  name: "",
                  value: "辽宁石油化工大学",
                },
                {
                  name: "",
                  value: "抚顺南站",
                },
                {
                  name: "",
                  value: "辽宁大学",
                },
              ],
            },
            {
              name: "人数",
              unit: "人",//此列的单位
              children: [
                {
                  name: "",
                  value: "342",
                },
                {
                  name: "",
                  value: "4554",
                },
                {
                  name: "",
                  value: "12565",
                },
                {
                  name: "",
                  value: "77684",
                },
                {
                  name: "",
                  value: "47",
                },
                {
                  name: "",
                  value: "6",
                },
              ],
            },
          ],
        },
      },
    };
  },
  mounted() {},
  methods: {},
};
</script>
<style scope lang="scss">
.dcv-txt-list {
  display: flex;
  flex-wrap: wrap;
  .module {
    width: 400px;
    height: 300px;
    border: 1px solid #ccc;
    margin: 12px;
    // padding: 24px;
    background: #011840;
  }
  .app-from {
    position: absolute;
    top: 0;
    right: 0px;
    height: 100vh;
    width: 300px;
    overflow-y: scroll;
  }
}
</style>
```
