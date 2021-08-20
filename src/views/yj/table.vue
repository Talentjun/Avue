<template>
  <div class="table">
    <el-table
      id="iTable"
      :data="data"
      ref="mutipleTable"
      @selection-change="handleSelectionChange"
      v-loading="isLoad"
      element-loading-text="数据正在加载中..."
      :show-summary="isShowSummary"
      :empty-text="emptyText"
      :border="border"
    >
      <!--region 数据列-->
      <template v-for="column in columns">
        <template v-if="column.type">
          <el-table-column
            :type="column.type"
            :key="column.label"
            :label="column.label"
            :align="column.align"
            :width="column.width"
          ></el-table-column>
        </template>
        <template v-else>
          <el-table-column
            :prop="column.prop"
            :key="column.label"
            :label="column.label"
            :align="column.align"
            :width="column.width"
          >
            <template slot-scope="scope">
              <slot
                :scope="scope.row"
                v-if="column.slot"
                :name="column.slot"
                :row="scope.row[column.slot]"
              />
              <span v-else>{{ scope.row[column.prop] }}</span>
            </template>
          </el-table-column>
        </template>
      </template>
      <!--endregion-->
    </el-table>
  </div>
</template>
<!--endregion-->
<script>
export default {
  props: {
    // 数据列表
    data: {
      type: Array,
      default: [],
    },
    // 需要展示的列 === prop：列数据对应的属性，label：列名，align：对齐方式，width：列宽, // table 表格的控制参数
    columns: {
      type: Array,
      default: [],
    },
    //是否加载
    isLoading: {
      type: Boolean,
      default: false,
    },
    //是否在表尾显示合计行
    isShowSummary: {
      type: Boolean,
      default: false,
      require: false,
    },
    //emptyText
    emptyText: {
      type: String,
      default: "暂无数据",
      require: false,
    },
    //是否带边框
    border: {
      type: Boolean,
      default: false,
      require: false,
    },
    //选择方式（仅用于多选时）
    type: {
      type: String,
      default: "select",   //select：多选    radio：单选
      require: false,
    },
  },
  // 数据
  data() {
    return {
      pageIndex: 1,
      multipleSelection: [], // 多行选中
      isLoad: this.isLoading,
    };
  },
  watch: {
    isLoading: function (val, old) {
      this.isLoad = val;
    },
  },
  methods: {
    // 多行选中
    handleSelectionChange(val) {
      this.multipleSelection = val;
      this.$emit("result", val);
    },
  },
};
</script>