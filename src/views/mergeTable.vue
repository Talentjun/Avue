<template>
  <div>
    <avue-crud
      :data="tableData"
      :option="tableOption"
      @on-load="tableOnLoad"
      :span-method="spanMethod"
      :row-class-name="rowClassName"
      @current-row-change="handleCurrentRowChange"
      @cell-mouse-enter="cellMouseEnter"
      @cell-mouse-leave="cellMouseLeave"
      ref="crud"
    ></avue-crud>
  </div>
</template>

<script>
export default {
  data() {
    return {
      spanArr: [], //合并单元格的数目
      sameRowArr: [], //为每一条数据添加一个index属性用来标识每行数据
      curRowArr: [], //存合并的行号相同的数据
      tableData: [
        {
          originId: 123,
          originTotalAmount: 456,
          id: 111,
        },
        {
          originId: 123,
          originTotalAmount: 456,
          id: 111,
        },
        {
          originId: 1234,
          originTotalAmount: 456,
          id: 222,
        },
      ],
      tableOption: {
        border: true,
        align: 'center',
        addBtn: false, // 不显示添加
        column: [
          {
            label: '原始订单编号',
            prop: 'originId',
          },
          {
            label: '原始订单金额',
            prop: 'originTotalAmount',
          },
          {
            label: '转单订单编号',
            prop: 'id',
          },
        ],
      },
    }
  },
  methods: {
    tableOnLoad() {
      this.spanArr = []
      this.sameRowArr = []
      let contactDot = 0
      let sIdx = 0
      this.tableData.forEach((item, index) => {
        if (index === 0) {
          this.spanArr.push(1)
          this.sameRowArr.push([index])
        } else {
          // 这里的originId取的是list集合第一个要合并的列的字段
          if (item.originId === this.tableData[index - 1].originId) {
            this.spanArr[contactDot] += 1
            this.spanArr.push(0)
            this.sameRowArr[sIdx].push(index)
          } else {
            contactDot = index
            this.spanArr.push(1)
            sIdx = sIdx + 1
            this.sameRowArr.push([index])
          }
        }
      })
    },
    // 合并的方法
    spanMethod({ rowIndex, columnIndex }) {
      // 合并操作列的下标要+1
      if (columnIndex === 0 || columnIndex === 2 || columnIndex === 4) {
        const _row = this.spanArr[rowIndex]
        const _col = _row > 0 ? 1 : 0
        // rowspan和colspan都为0表示 隐藏该单元格。这里必须有，否则单元格会被右移一列
        return {
          rowspan: _row,
          colspan: _col,
        }
      }
    },
    // hover背景颜色变化
    rowClassName({ row, rowIndex }) {
      let temArr = this.curRowArr
      for (let i = 0; i < temArr.length; i++) {
        if (rowIndex == temArr[i]) {
          // 默认hover-row 这里要用row_class的样式覆盖它
          return 'row_class'
        }
      }
    },
    cellMouseEnter(row) {
      this.sameRowArr.map((item) => {
        if (item.indexOf(row.$index) != -1) {
          this.curRowArr = item
        }
      })
    },
    cellMouseLeave() {
      this.curRowArr = []
    },
    handleCurrentRowChange(row) {
      this.sameRowArr.map((item) => {
        if (item.indexOf(row.$index) != -1) {
          this.curRowArr = item
        }
      })
      this.$refs.crud.setCurrentRow(row)
    },
  },
}
</script>

<style lang="scss" scoped>
::v-deep .row_class > td {
  background-color: #f5f7fa;
}
::v-deep .row_click_class > td {
  background: rgba(110, 211, 248, 1);
}
</style>