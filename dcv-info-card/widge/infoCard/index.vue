<!--
 * @Descripttion: 
 * @version: 
 * @Author: cholee
 * @Date: 2019-08-01 15:31:01
 * @LastEditors: cholee
 * @LastEditTime: 2020-08-27 10:03:43
-->
<template>
  <a-card
    hoverable :bodyStyle="bodyStyle"
    style="width:300px;display:inline-block;margin:10px 0 10px 10px" 
  >
    <div class="card-status" style="height:64px">
         <timeCount :startDate="cardStatus.startDate"></timeCount>
    </div>
    <a-card-meta style="margin:0;padding: 10px" 
      :title="cardStatus.stateName"
      :description="cardStatus.description"
      >
      <a-avatar shape="square" :size="64"  slot="avatar" :src="require('./assets/logo.png')"/>
    </a-card-meta>

    <div class="card-bottom">
        <span class="card-deal">{{cardStatus.dealStatus}}</span>
        <span class="card-part">{{cardStatus.department}}</span>
    </div>
  </a-card>
</template>

<script>
/**
 * @author lichao
 * @version 1.0.3
 * @description 监测预警对象卡片信息组件
 * @update 2019.8.10
 * @memo 与正常组件使用方法一致，详情参考App.vue
 * [注：其中TODO为组件需要实现的逻辑]
 */
// 引用文件
import './js/index'
import timeCount from './components/timeCount.vue'
export default {
  components:{timeCount},
  name: 'infoCard',
  props:{"cardStatus":Object},
  data() {
    return {
        bodyStyle:{"padding":0}
    }
  },
  methods:{

  }
}
</script>

<style lang="scss" scoped>
//**  /deep/深度渗透，解决父组件样式不会渗透到子组件
/deep/ .ant-card-meta-avatar{
  padding-right: 10px;
}
@import './style/index.scss';
</style>
