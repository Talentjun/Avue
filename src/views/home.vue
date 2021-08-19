<template>
  <div>
    <basic-container>
      <h3>关键数据</h3>
      <div>
        <span style="margin-right:10px;">充值市场订单结算时间</span>
        <el-date-picker
          v-model="time"
          type="daterange"
          start-placeholder="开始时间"
          end-placeholder="结束时间"
          size="small"
          class="mr10"
        ></el-date-picker>
        <span
          :class="active == index ? 'mr10 blue' : 'mr10'"
          v-for="(item, index) in datetime"
          :key="item.value"
          @click="setTime(item.value, index)"
          >{{ item.name }}</span
        >
        <el-button type="primary" size="small" @click="handleSearch"
          >查询</el-button
        >
        <el-button size="small" @click="time = []">清空</el-button>
      </div>
    </basic-container>
  </div>
</template>

<script>
import dayjs from 'dayjs'
export default {
  data() {
    return {
      time: [],
      datetime: [
        { name: '昨日', value: 'yestarday' },
        { name: '今日', value: 'day' },
        { name: '上周', value: 'lastweek' },
        { name: '本周', value: 'week' },
        { name: '本月', value: 'month' },
        { name: '全年', value: 'year' },
      ],
      active: 4,
    }
  },
  methods: {
    handleSearch() {
      if (this.time == null) this.time = []
    },
    // 设置搜索时间
    setTime(s, index) {
      this.active = index
      if (s === 'yestarday') {
        let start = new Date(dayjs().subtract(1, 'day').startOf('day'))
        let end = new Date(dayjs().subtract(1, 'day').endOf('day'))
        this.time = [start, end]
        this.handleSearch()
        return
      } else if (s === 'lastweek') {
        let start = new Date(
          dayjs().subtract(1, 'week').startOf('week').add(1, 'day')
        )
        let end = new Date(
          dayjs().subtract(1, 'week').endOf('week').add(1, 'day')
        )
        this.time = [start, end]
        this.handleSearch()
        return
      } else if (s === 'week') {
        let start = new Date(dayjs().startOf(s).add(1, 'day'))
        let end = new Date(dayjs().endOf(s).add(1, 'day'))
        this.time = [start, end]
        this.handleSearch()
        return
      }
      let start = new Date(dayjs().startOf(s))
      let end = new Date(dayjs().endOf(s))
      this.time = [start, end]
      this.handleSearch()
    },
  },
}
</script>

<style lang="scss" scoped>
.mr10 {
  margin-right: 10px;
  cursor: pointer;
}
.blue {
  color: #5bc6f5;
}
.date-wrap {
  border: 1px solid rgba(233, 233, 233, 1);
  border-radius: 4px;
  padding: 20px;
  .grey {
    color: #929292;
  }
  .num {
    font-size: 30px;
    color: black;
    display: flex;
    justify-content: space-between;
    align-items: flex-end;
    .el-icon-top{
      color: #D9001B;
      font-size: 12px;
      text-align: right;
    }
    .el-icon-bottom{
      color: #70B603;
      font-size: 12px;
      text-align: right;
    }
  }
}
</style>