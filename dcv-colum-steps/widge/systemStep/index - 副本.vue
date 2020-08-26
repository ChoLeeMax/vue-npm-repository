<template>
  <div class="step">
      <div ref="line" class="step-line">
        <div ref="inline" class="step-inline"></div>
      </div>
      <!-- 主内容 -->
      <div class="step-list">
          <div class="step-item" v-for="(item,index) in stepData" :key="index">
              <div class="setpNorm" :class="{stepActive:item.status=='1',stepNone:item.status=='0'}">
                  <div class="step-back">
                       <img class="step-img" v-if="item.status=='1'" :src="activeSvg">
                  </div>
                  <div class="step-title">{{item.title}}</div>
              </div>
              <div class="step-content">
                  <div class="step-time">{{item.time}}</div>
                  <div class="step-user">{{item.user}}</div>
                  <div class="step-info">{{item.info}}</div>
              </div>
          </div>
      </div>
  </div>
  
</template>


<script>
/**
 * @author lichao
 * @version 1.0.9
 * @description  处置流程组件
 * @update 2019.9.3
 * @memo 正常组件使用，参考App.vue
 * [注：其中TODO为组件需要实现的逻辑]
 */
// 引用文件
// import activeSvg from './assets/active.svg'
import './js/index'
import 'dc-style'
export default {
  name: 'dcv-systemstep',
  // TODO 设置动态属性
  data() {
    return {
        horiWidth:null,
        activeSvg:require('./assets/active.svg')
    }
  },
  props:[
    "steps",
    "stepData"
  ],
  watch: {
     steps(val){
        this.setLine(this.steps);
     } 
  },
  methods:{
    setLine(steps){
        let total=this.stepData.length;
        let step= parseInt(steps);
        if(step==0||total==1){
            return;
        }
        let percent=100-step/(total-1)*100;
        this.$refs.line.style.height=(total-1)*160+12+"px";
        this.$refs.inline.style.bottom=percent+"%";
    },
    getMaxWidth(doms){
        var maxWidth=0;
        for (const dom of doms) {
            let w=dom.offsetWidth;
            if (w>maxWidth) {
                maxWidth=w;
            }
        }
        for (const dom of doms) {
            dom.style.width=maxWidth+'px';
        }
    },
  },
  mounted(){
        this.setLine(this.steps);

  }
}
</script>

<style lang="scss" scope>
@import './style/index.scss';
@import 'dc-style';
.step{
  position: relative !important;
  height: auto;
  font-size:14px;
  width: 100%;
  font-family:PingFangSC;
  font-weight:400;
  .step-line {
      position: absolute; 
      z-index: 5;
      top: 1px;
    //   bottom: -12px;
      left: 19px;
      width: 1px;
      background-color: #CCCCCC;
      .step-inline {
        position: absolute; 
        top: 1px;
        // bottom: 0;
        left: 0px;
        width: 1px;
        background-color:#1890FF;
      }
  }
  .step-list{
      .step-item:last-child{
          height: auto;
      }
      .step-item{
          height: 160px;
          display: flex !important;
          .step-content{
              flex: 1 !important;
          }
          .setpNorm{

          }
          .step-content{
              .step-time{
                  color:#999999;
                  padding: 0 0 6px 0;
                  line-height: 14px;
                  border-bottom: solid 1px #EDEDED;
              }
              .step-user{
                  font-size:18px;
                  font-weight:500;
                  line-height: 18px;
                  margin: 16px 0 24px 0;
                  color:#333333;
              }
              .step-info{
                  line-height: 14px;
                  color:#666666;
              }
          }
          .stepActive{
              display: flex;
              .step-back{
                  width:40px;
                  height:40px;
                  border-radius: 40px;
                  background: #1890FF;
                  z-index: 11;
                  .step-img{
                      vertical-align: unset;
                      margin-top: 12.5px;
                      margin-left: 9px;
                  }
              }
              .step-title{
                  margin: 0 44px 0 16px;
                  color:#1890FF;
                  letter-spacing:1px;
                  width: 30px;
                  padding-top: 10px;
              }
          }
          .stepNone{
              display: flex;
              .step-back{
                  width: 16px;
                  height: 16px;
                  border-radius: 16px;
                  background: #CCCCCC;
                  margin:12px 0 0 12px;
              }
              .step-title{
                  line-height: 40px;
                  margin: 0 44px 0 28px;
                  color:#999999;
                  letter-spacing:1px;
              }
            }
      }
  }
}


</style>
