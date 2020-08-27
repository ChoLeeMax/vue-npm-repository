<!--
 * @Descripttion: 
 * @version: 
 * @Author: cholee
 * @Date: 2019-08-06 15:30:02
 * @LastEditors: cholee
 * @LastEditTime: 2020-08-27 09:58:06
-->
<template>
  <div class="container">
    <div class="timeBox bg" title="超时预警">{{start}}</div>
  </div>
</template>

<script>
export default {
  components: {},
  props: ["startDate"],
  data() {
    return {
      start: this.startDate,
    };
  },
  methods: {
    setTimer() {
      let splitDate = this.start.split(":");
      this.minu = parseInt(splitDate[0]);
      this.secd = parseInt(splitDate[1]);
      var minuTimer = setInterval(() => {
        this.secd++;
        if (this.secd < 10) {
          this.secd = "0" + this.secd;
        }
        if (this.minu < 10) {
          this.minu = "0" + parseInt(this.minu);
        }
        if (this.secd == 60) {
          this.minu++;
          this.minu = "0" + this.minu;
          this.secd = "0" + 0;
        }
        this.start = this.minu + ":" + this.secd;
      }, 1000);
    },
  },
  created() {
    this.setTimer();
  },
  mounted() {},
};
</script>


<style lang="scss" scoped>
.container {
  .timeBox {
    background: red;
    color: #ffffff;
    padding: 0 6px;
  }
}
</style>