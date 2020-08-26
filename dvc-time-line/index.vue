    <div class="line-wrap">
      <div class="x-line">
        <div class="line-item" v-for="line in lineList" :key="line"></div>
      </div>
      <div class="x-name">
        <div class="name-item" v-for="(line,i) in lineList" :key="i">
          <span class="zero" v-if="i===0">0时</span>
          <span class="number">{{line}}</span>
        </div>
      </div>
    </div>
	
	
	      lineList: [
        "2时",
        "4时",
        "6时",
        "8时",
        "10时",
        "12时",
        "14时",
        "16时",
        "18时",
        "20时",
        "22时"
      ],
	
	
	.line-wrap {
    position: absolute;
    left: 5%;
    right: 5%;
    bottom: 400px;
    z-index: 1;
    .x-line {
      height: 2px;
      background: #c1eaf7;
      display: flex;
      justify-content: space-between;
      align-items: flex-end;
      .line-item {
        flex: 1;
        height: 50px;
        position: relative;
        border-left: solid 2px #c1eaf7;
      }
      .line-item::before {
        display: block;
        width: 2px;
        height: 25px;
        background: #c1eaf7;
        position: absolute;
        left: 50%;
        content: "";
        bottom: 2px;
      }
      .line-item:last-child {
        border-right: solid 2px #c1eaf7;
      }
    }
    .x-name {
      display: flex;
      justify-content: space-between;
      align-items: flex-end;
      .name-item {
        flex: 1;
        font-size: 48px;
        font-family: Microsoft YaHei;
        font-weight: 400;
        text-align: right;
        color: #82acc6;
        .zero {
          float: left;
          margin-left: -32px;
        }
        .number {
          display: inline-block;
        //   width: 78px;
          position: relative;
          transform: translateX(44px);
        }
      }
    }
  }
  