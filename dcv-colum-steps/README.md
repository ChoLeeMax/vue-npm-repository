## 工程介绍

修改 package 配置文件组件名称(name)、描述(description)、版本(version)、入口文件（main）；

修改组件目录下的 vue 布局文件，调整为实际组件布局；

修改组件目录下的 js 脚本文件，调整为实际组件实现逻辑；

修改组件目录下的 scss 样式文件，调整为实际组件样式内容；

将组件所需的资源文件放在组件目录下的 assets 文件夹下，注意引用路径；

修改根目录下的组件测试入口文件 index.vue，调整为实际组件调用方式；

修改根目录下的工程配置文件,调整组件名称(name)、描述(description)、版本(version)、入口文件（main）字段；

## 发布组件
在组件dcv-colum-steps目录执行
```js
npm publish
```

## 组件使用

- 安装组件

```js
    npm i dcv-colum-steps
```

- 使用组件

```
<!--
 * @Descripttion: 
 * @version: 
 * @Author: cholee
 * @Date: 2019-09-03 17:28:48
 * @LastEditors: cholee
 * @LastEditTime: 2020-08-26 15:23:31
-->
<template>
  <div class="stepwrap">
      <!-- 使用组件 -->
      <systemStep :steps="steps" :stepData="stepData" v-if="stepData.length>0"></systemStep>
  </div>
</template>

<script>
// 使用 npm i dcv-colum-steps 命令安装引用
// import systemStep from 'dcv-colum-steps';
//绝对路径引用，需拷贝组件文佳至本地
// import systemStep from "./dcv-colum-steps/widge/index.js";
/**
 * @author lichao
 * @version 1.0.0
 * @description 系统处置流程组件
 */
export default {
  name: 'App',
  // 注册组件
    components: { systemStep },
    data() {
        // TODO 初始化数据
        return {
           steps:1,//步骤数
           stepData:[{
              status:"1",//状态
              title:"开始",
              time:"2019年05月16日  8:00",
              user:"领导1",
              info:"AQI预警线100，当前AQI123，高于预警线！"
           }
           ,{
              status:"1",
              title:"处理中",
              time:"2019年05月17日  8:00",
              user:"领导2",
              info:"AQI预警线100，当前AQI123，高于预警线！"
           },{
              status:"0",
              title:"处理完成的说法",
              time:"2019年05月18日  8:00",
              user:"领导3",
              info:""
           }
           ]
        }
    }
}
</script>
<style lang="scss">
   .stepwrap{
      // height: 300px;
      width: 40%;
      position: relative;
   }
</style>

```
