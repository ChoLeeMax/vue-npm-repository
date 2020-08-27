## 工程介绍

修改 package 配置文件组件名称(name)、描述(description)、版本(version)、入口文件（main）；

修改组件目录下的 vue 布局文件，调整为实际组件布局；

修改组件目录下的 js 脚本文件，调整为实际组件实现逻辑；

修改组件目录下的 scss 样式文件，调整为实际组件样式内容；

将组件所需的资源文件放在组件目录下的 assets 文件夹下，注意引用路径；

修改根目录下的组件测试入口文件 index.vue，调整为实际组件调用方式；

修改根目录下的工程配置文件,调整组件名称(name)、描述(description)、版本(version)、入口文件（main）字段；

## 发布组件
在组件dcv-ant-table目录执行
```js
npm publish
```

## 组件使用

- 安装组件

```js
    npm i dcv-ant-table
```

- 使用组件

```
<!--
 * @Descripttion: 基于ant的表格组件封装
 * @version: 
 * @Author: cholee
 * @Date: 2019-09-29 16:07:18
 * @LastEditors: cholee
 * @LastEditTime: 2020-08-27 14:09:00
-->
<template>
  <div>
    <!-- 使用组件 -->
    <eventTable
      :columns="columns"
      :dataSource="dataSource"
      :rowKey="rowKey"
      :border="border"
      :trClass="trClass"
      @trClick="trClick"
      @onSwitch="onSwitch"
      :paginations="paginations"
      @paginationChange="paginationChange"
    ></eventTable>
  </div>
</template>

<script>
import eventTable from "./src/widge/index.js";
/**
 * @author lichao
 * @version 1.0.3
 * @description 表格组件使用和测试
 */
// TODO 引用组件
// 使用 npm i dcv-ant-table 命令安装引用
// import pieChart from 'dcv-ant-table';
//绝对路径引用，需拷贝组件文佳至本地
// import pieChart from "./dcv-ant-table/widge/index.js";

const columns = [
  {
    title: "编号",
    width: "200px", //列宽
    align: "center", //文字水平居中
    dataIndex: "unicode",
  },
  {
    title: "名称",
    dataIndex: "money",
  },
  {
    title: "内容",
    dataIndex: "address",
  },
  {
    title: "开关",
    dataIndex: "switch",
    scopedSlots: { customRender: "switch" },
  },
  {
    title: "状态",
    key: "state",
    dataIndex: "status",
    scopedSlots: { customRender: "status" },
  },
  {
    title: "操作",
    dataIndex: "actions",
    key: "actions",
    scopedSlots: { customRender: "actions" },
  },
];

let dataSource = [
  {
    unicode: "1",
    money: "供电站",
    address: "南山大道",
    switch: true,
    statusCode: "success",
    status: "已处理",
    actions: [{ name: "详情" }],
  },
  {
    unicode: "2",
    money: "供水站",
    address: "林肯公园",
    switch: true,
    statusCode: "error",
    status: "未处理",
    actions: [{ name: "详情" }, { name: "重置", color: "red" }],
  },
  {
    unicode: "3",
    switch: false,
    money: "供气站",
    address: "怡宝小区",
    statusCode: "warning",
    status: "处置中",
    actions: [
      { name: "详情" },
      { name: "重置", color: "red" },
      { name: "跳转", color: "#FFEB3B" },
    ],
  },
];
export default {
  name: "App",
  // 注册组件
  components: { eventTable },
  data() {
    // TODO 初始化数据
    return {
      border: false, //是否显示外边框，默认不传为true
      trClass: "trClass",//自定义行样式
      rowKey: "unicode", //制定组件内部key值,具备唯一性
      // paginations:false,//设置为flase，不显示分页
      paginations: {
        total: 50, //总数
        current: 1, //选择页数
        pageSize: 5, //页码总数
      },
      columns: columns,//表头
      dataSource: dataSource,//数据
    };
  },
  methods: {
    //表格行点击
    trClick(record) {
      //record.text属性用来区分操作按钮
      console.log(record);
    },
    //分页组件点击,paginations为false不设置
    paginationChange(pagination) {
      console.log(pagination);
    },
    //行开关Switch事件
    onSwitch(checked, record) {
      console.log(checked);
    },
  },
};
</script>
<style lang="scss">
//自定义tr样式
.trClass {
  // background: red;
}
</style>

```
