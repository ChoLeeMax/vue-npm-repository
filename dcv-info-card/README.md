<!--
 * @Descripttion: 监测预警计时卡片
 * @version:
 * @Author: cholee
 * @Date: 2020-06-09 16:52:04
 * @LastEditors: cholee
 * @LastEditTime: 2020-08-27 10:12:29
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
在组件dcv-info-card目录执行
```js
npm publish
```

## 组件使用

- 安装组件

```js
    npm i dcv-info-card
```

- 使用组件

```
<template>
  <div class="">
      <!-- 使用组件 -->
     <infoCard v-for="item in dataList" :key="item.stateName" :cardStatus="item"></infoCard> 
  </div>
</template>

<script>

/**
 * @author lichao
 * @version 1.0.3
 * @description 组件使用和测试
 */
// TODO 引用组件
// 使用 npm i dcv-info-card 命令安装引用
// import infoCard from 'dcv-info-card';
//绝对路径引用，需拷贝组件文佳至本地
// import infoCard from "./dcv-info-card/widge/index.js";

export default {
  name: 'App',
  // 注册组件
    components: { infoCard },
    data() {
        // TODO 初始化数据
        return {
          dataList:[{
            startDate:"01:00",
            stateName:"怡众名称供热站",
            description:"1次供水温度",
            dealStatus:"处理中",
            department:"水电局"
          },{
            startDate:"00:30",
            stateName:"平成供电所",
            description:"1次供电",
            dealStatus:"处理中",
            department:"水电局"
          }],
        }
    }
}
</script>
```
