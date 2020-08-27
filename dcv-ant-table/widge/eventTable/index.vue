<template>
  <div class="dcv-table">
    <a-locale-provider :locale="zhCN">
      <a-table
        :columns="columns"
        :dataSource="dataSource"
        :bordered="border===false?border:true"
        :rowClassName="rowClass"
        :rowKey="rowKey"
        :pagination="pagination"
        @change="paginationChange"
        :rowSelection="rowSelection"
      >
        <span slot="status" slot-scope="text,record">
          <a-badge :status="record.statusCode" />
          {{record.status}}
        </span>
        <span slot="actions" slot-scope="actions,record">
          <a
            class="action"
            v-for="item in actions"
            :key="item.name"
            :style="{color:item.color?item.color:'blue'}"
            @click="changeHande(item,record)"
          >{{item.name}}</a>
        </span>
        <span slot="switch" slot-scope="switchBt,record">
          <a-switch
            :defaultChecked="switchBt"
            @change="function(checked){onChangeSwitch(checked,record)}"
          />
        </span>
      </a-table>
    </a-locale-provider>
  </div>
</template>
<script>
/**
 * @author lichao
 * @version 1.0.2
 * @description 全部预警列表table组件
 * @update 2019.8.7
 * @memo  与正常组件使用方法一致，详情参考App.vue
 * [注：其中TODO为组件需要实现的逻辑]
 */
// 引用文件
import "./js/index";
import zhCN from "ant-design-vue/lib/locale-provider/zh_CN";
import { Table, LocaleProvider } from "ant-design-vue";
export default {
  name: "dcv-eventTable",
  components: { aTable: Table, aLocaleProvider: LocaleProvider },

  // TODO 设置动态属性
  data() {
    return {
      zhCN,
      defPagination: {
        showTotal: function(total) {
          return `共 ${total} 条数据`;
        },
        showSizeChanger: true, //是否显示页码数
        showQuickJumper: true, //是否显示跳转页码按钮
        size: "small",
        defaultPageSize: 10, //默认每页显示条数
        pageSize: 10, //每页显示条数
        pageSizeOptions: ["10", "20", "30", "40"] //每页条数
      }
    };
  },
  // TODO 设置用于接收父组件传来的数据
  props: [
    "columns",
    "dataSource",
    "rowKey",
    "paginations",
    "rowSelection",
    "border",
    "trClass"
  ],
  watch: {
    paginations(val) {
      if (val) {
        this.pagination = Object.assign({}, this.pagination, val);
      } else {
        this.pagination = false;
      }
    }
  },
  created() {
    if (this.paginations) {
      this.pagination = Object.assign({}, this.defPagination, this.paginations);
    } else {
      this.pagination = false;
    }
  },
  methods: {
    paginationChange(pagination) {
      this.$emit("paginationChange", pagination);
    },
    // 自定义行样式
    rowClass(record, index) {
      if (this.trClass) {
        return this.trClass;
      } else {
        if (parseInt(index) % 2 == 1) {
          return "rowClass";
        }
      }
    },
    //当前行操作
    changeHande(item, record) {
      record.text = item.name;
      this.$emit("trClick", record);
    },
    onChangeSwitch(checked, record) {
      this.$emit("onSwitch", checked, record);
    }
  }
};
</script>

<style lang="scss" scope>
// @import "./style/index.scss";
.dcv-table .rowClass {
  background: #fafafa;
  transition: background 0.3s ease;
}
.ant-table-row .action {
  color: #1890ff;
  margin-right: 16px;
}

.dcv-table /deep/ .ant-pagination.mini .ant-pagination-total-text {
  float: left;
  font-family: PingFangSC;
  font-weight: 400;
  color: rgba(153, 153, 153, 1);
}

.dcv-table /deep/ .ant-table-pagination.ant-pagination {
  margin: 0;
  padding: 16px;
  float: none;
  text-align: right;
  background: #fafafa;
  border-bottom: solid 1px #e8e8e8;
}
</style>
