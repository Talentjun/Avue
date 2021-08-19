<template>
  <basic-container>
    <div
      id="main"
      style="width: 600px; height: 400px; border: 1px solid red"
    ></div>
  </basic-container>
</template>

<script>
import * as echarts from 'echarts'
export default {
  mounted() {
    // 基于准备好的dom，初始化echarts实例
    var myChart = echarts.init(document.getElementById('main'))
    let echartData = [
      {
        value: 0,
        name: '30%',
        itemStyle: {
          color: 'rgb(79,121,189)',
        },
        tooltip: {
          formatter:
            '<p style="text-align:center">竞价成功概率较高<br />{b}</p>',
        },
      },
      {
        value: 0,
        name: '20%',
        itemStyle: {
          color: 'rgb(155,187,89)',
        },
        tooltip: {
          formatter:
            '<p style="text-align:center">竞价成功概率中等<br />{b}</p>',
        },
      },
      {
        value: 45,
        name: '45%',
        itemStyle: {
          color: 'rgb(192,80,77)',
        },
        tooltip: {
          formatter:
            '<p style="text-align:center">竞价成功概率较低<br />{b}</p>',
        },
      },
    ]
    let filterData = echartData.filter((item) => item.value != 0)
    // 指定图表的配置项和数据
    var option = {
      animation: false, // 不展示渲染动画
      tooltip: {
        trigger: 'item', // tooltip前提条件
      },
      series: [
        {
          type: 'pie',
          radius: '55%',
          center: ['50%', '50%'],
          // hoverAnimation: false,
          data: filterData,
          label: { position: 'inside', color: 'black' }, // 将name展示在里面 且颜色为黑色
          itemStyle: { borderWidth: 1, borderColor: '#fff' },
        },
      ],
    }

    // 使用刚指定的配置项和数据显示图表。
    myChart.setOption(option)
  },
}
</script>

<style lang="scss" scoped>
</style>