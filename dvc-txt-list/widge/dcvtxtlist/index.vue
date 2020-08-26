<template>
  <div class="dcv-warp">
    <div class="dcv-list">
      <div class="list-header" :style="{'background':rowColors[0]}">
        <div class="list-item" v-for="head in information.data" :key="head.name">{{head.name}}</div>
      </div>
      <div
        class="list-row"
        v-for="(row,index) in rowData"
        :key="row.value"
        :style="{'background':rowColors[index+1]}"
      >
        <div class="list-item" v-for="item in information.data" :key="item.name">
          <!-- <span class="name" v-if="item.children[index].name">{{item.children[index].name+'：'}}</span> -->
          {{item.children[index].value}}
          <span class="unit" v-if="item.unit">{{item.unit}}</span>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
/**
 * @author lichao
 * @version 1.0.2
 * @description
 * @update 2020-6-12 更新组件输入数据格式(大屏组件数据格式3)
 * @memo 正常组件使用，参考App.vue
 * [注：其中TODO为组件需要实现的逻辑]
 */
// 引用文件
import { MathTraversal } from "dc-math";
import "./js/index";
// 主题颜色
import mixin from "dc-style/src/mixin.js";
export default {
  name: "dcv-demo",
  // TODO 设置动态属性
  data() {
    return {
      rowData: [], //行数据
      rowColors: [],
      rowOpacity: [1, 0.5, 0.4, 0.3, 0.25, 0.2],
      config: {
        fontSize: 16,
        themeColor: "#2196f3"
      },
    };
  },
  mixins: [mixin],
  // TODO 设置用于接收父组件传来的数据
  props: {
    configuration: {
      type: Object,
      default: () => {
        return {};
      },
    },
    information: Object,
  },
  watch: {
    /**
     * 监听图形数据变化
     * @param {更新后的数据} data
     */
    information(data) {
      this.setData(data);
    },
  },
  methods: {
    /**
     * 处理成符合渲染的数据
     */
    setData(information) {
      information = information || this.information;
      const data = information.data;
      this.rowData = data[0].children;
      //处理配置
      this.config = Object.assign(this.config, this.configuration);
      this.rowColors = [];
      const themeColor = this.config.themeColor;
      let length = data[0].children.length + 2;
      for (let index = 0; index < length; index++) {
        let opacity = this.rowOpacity[index];
        if (!opacity) {
          opacity = 0.2;
        }
        this.rowColors.push(this.hexToRgba(themeColor, opacity));
      }
    },
    hexToRgba(hex, opacity) {
      return (
        "rgba(" +
        parseInt("0x" + hex.slice(1, 3)) +
        "," +
        parseInt("0x" + hex.slice(3, 5)) +
        "," +
        parseInt("0x" + hex.slice(5, 7)) +
        "," +
        opacity +
        ")"
      );
    },
  },
  created() {},

  mounted() {
    if (this.information != {}) this.setData(this.information);
  },
};
</script>

<style lang="scss" scope>
.dcv-warp ::-webkit-scrollbar {
  width: 6px;
  height: 6px;
  background-color: #214d90;
}
.dcv-warp ::-webkit-scrollbar-thumb {
  width: 2px;
  height: 16px;
  border: 1px solid rgba(59, 103, 170, 1);
  border-radius: 2px;
  background-color: #204173;
}
.dcv-warp {
  height: 100%;
  width: 100%;
}
.dcv-list {
  font-size: 16px;
  font-family: Microsoft YaHei;
  font-weight: 400;
  color: #aaeaff;
  // line-height: 30px;
  overflow-y: auto;
  height: 100%;
  width: 100%;

  display: flex;
  flex-direction: column;
  .list-header {
    display: flex;
    flex: 0.8;
    align-items: center;
  }
  .list-row {
    margin-top: 7px;
    display: flex;
    flex: 1;
    align-items: center;
  }
  .list-item {
    flex: 1;
    text-align: center;
    height: 40px;
    line-height: 40px;
    word-break: keep-all;
    .unit {
      margin-left: -8px;
    }
  }
}
</style>
