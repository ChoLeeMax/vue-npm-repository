<template>
  <div class="headWrap">
    <img class="logo" v-if="logoShow" :src="logoSvg" />
    <ul class="nav-list">
      <li
        v-for="(item, index) in navList"
        :key="item.label"
        @click.prevent="navClick(item, index, $event)"
        :style="{ position: item.soltwidth == 'li' ? 'relative' : 'unset' }"
        :class="['nav-item', { navActive: index == activeIndex }]"
      >
        <img v-if="item.icon" class="nav-icon sel" :src="item.icon" />
        <a class="tiltle">{{ item.label }}</a>
        <div v-if="item.subConmpent" class="subConmpent" ref="headSlot">
          <slot :name="item.subConmpent"></slot>
        </div>
      </li>
    </ul>
    <svg class="filter" height="100%" width="100%" xmlns="http://www.w3.org/2000/svg">
      <defs>
        <!-- 白色 -->
        <filter id="white">
          <feColorMatrix
            type="matrix"
            values="
                    0 0 0 0 1
                    0 0 0 0 1
                    0 0 0 0 1
                    0 0 0 1 0"
          />
        </filter>
      </defs>
    </svg>
  </div>
</template>

<script>
/**
 * @author lichao
 * @version 1.0.3
 * @description 系统头部组件
 * @update 2019-7-25
 * @memo 正常组件使用，参考App.vue
 * [注：其中TODO为组件需要实现的逻辑]
 */
// 引用文件
import "./js/index";
import { Divider } from "ant-design-vue";

export default {
  name: "systemHead",
  components: { aDivider: Divider },
  // TODO 设置动态属性
  data() {
    return {
      logoShow: true,
      activeIndex: 0,
    };
  },
  // TODO 设置用于接收父组件传来的数据
  props: {
    logoSvg: String,
    urls: Object,
    navList: Array,
  },
  created() {
    // 拦截路由
    this.pathList = [];
    for (let i = 0; i < this.navList.length; i++) {
      this.pathList.push(this.navList[i].path);
    }
    if (this.$router) {
      if (this.$router) {
        this.$router.afterEach((to, from) => {
          // 判断是否是自己关系的路由
          const { path } = to;
          for (let i = 0; i < this.navList.length; i++) {
            const paths = this.navList[i].path;
            if (path === paths) {
              this.activeIndex = i;
            }
          }
        });
        const path = this.$router.history.current.fullPath;
        for (let i = 0; i < this.navList.length; i++) {
          const paths = this.navList[i].path;
          if (path === paths) {
            this.activeIndex = i;
          }
        }
      }
    }
  },
  methods: {
    /**
     * 头部导航菜单点击事件
     * @param {Object} item 当前数据对象
     * @param {Number} index 菜单索引
     * @param {Object} $event 点击事件默认对象
     * */
    navClick(item, index, $event) {
      if (
        $event.target.tagName == "A" ||
        $event.target.classList == "nav-item"
      ) {
        //一级菜单
        this.activeIndex = index;
        item.index = index;
        this.$emit("changeHand", item);
      } else if ($event.target.tagName == "LI") {
        //子菜单不执行
      }
    },
    /**
     * 根据索引关闭对应插槽
     * @param {Object} item 当前数据对象
     * */
    closeSlot(index) {
      if (this.$refs.headSlot) {
        if (isNaN(index)) {
          index = 0;
        }
        this.$refs.headSlot[index].classList.add("toggle");
      }
      setTimeout(() => {
        this.$refs.headSlot.map((item, index) => {
          item.classList.remove("toggle");
        });
      }, 1000);
    },
  },
};
</script>

<style scoped lang="scss">
@import "dc-style";
@import "./style/index.scss";
.headWrap {
  position: relative;
  .filter {
    display: none;
  }
}
.nav-list .nav-item .subConmpent {
  display: none;
  position: absolute;
  z-index: 999;
  top: 64px;
  left: 0;
  right: 0;
  height: auto;
}
.nav-list .nav-item:hover .subConmpent {
  display: block;
}
.nav-list .nav-item.navActive .toggle {
  display: none;
}
.nav-list .navActive .sel {
  filter: url(#white);
}
</style>
