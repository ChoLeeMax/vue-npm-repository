## 工程介绍

修改 package 配置文件组件名称(name)、描述(description)、版本(version)、入口文件（main）；

修改组件目录下的 vue 布局文件，调整为实际组件布局；

修改组件目录下的 js 脚本文件，调整为实际组件实现逻辑；

修改组件目录下的 scss 样式文件，调整为实际组件样式内容；

将组件所需的资源文件放在组件目录下的 assets 文件夹下，注意引用路径；

修改根目录下的组件测试入口文件 index.vue，调整为实际组件调用方式；

修改根目录下的工程配置文件,调整组件名称(name)、描述(description)、版本(version)、入口文件（main）字段；

## 发布组件
在组件dcv-row-header目录执行
```js
npm publish
```

## 组件使用

- 安装组件

```js
    npm i dcv-row-header
```

- 使用组件

```
<template>
  <div>
    <!-- 使用组件 -->
    <systemHead
      :logoSvg="logoSvg"
      :navList="navList"
      :urls="urls"
      @changeHand="changeHand"
      ref="headObj"
    >
      <div slot="location2" @click.stop="hideSolt" style="background:#54BFFF;color:#ffffff;font-size:16px">
        <div>sub menu1</div>
        <div>sub menu2</div>
        <div>sub menu3</div>
      </div>
    </systemHead>
  </div>
</template>

<script>
/**
 * @author lichao
 * @version 1.0.3
 * @description 组件使用和测试
 */
//此处可换成自己的图片
import logoSvg from "./assets/logo.svg";
import iconSvg from "./assets/icon.svg";

// 使用 npm i dcv-row-header 命令安装引用
// import systemHead from 'dcv-row-header';
//绝对路径引用，需拷贝组件文佳至本地
// import systemHead from "./dcv-row-header/widge/index.js";

export default {
  name: "App",
  // 注册组件
  components: { systemHead },
  data() {
    // TODO 初始化数据
    return {
      logoSvg: logoSvg,
      navList: [
        {
          label: "location-1",
          icon: iconSvg,
          path: "/index" //路由
        },
        {
          label: "location-2",
          icon: iconSvg,
          path: "",
          subConmpent: "location2",
          soltwidth: "li" //插槽宽度根据需求设置，li继承菜单宽度,head继承整个头部宽度,默认值head
        },
        {
          label: "location-3",
          icon: iconSvg,
          path: ""
        },
        {
          label: "location-4",
          icon: iconSvg,
          path: ""
        },
        {
          label: "location-5",
          icon: iconSvg,
          path: ""
        }
      ]
    };
  },
  methods: {
    changeHand(item) {
      console.log(item.label + item.index);
    },
    //关闭当前插槽;
    hideSolt() {
      this.$refs.headObj.closeSlot(); //不传index默认关闭第一个人插槽
      this.$refs.headObj.activeIndex = 1;//高亮当前父菜单
    }
  }
};
</script>

```
