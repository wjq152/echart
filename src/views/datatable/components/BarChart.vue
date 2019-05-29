<template>

  <div :class="className" :style="{height:height,width:width}" />
  
</template>

<script>
import echarts from 'echarts'
require('echarts/theme/macarons') // echarts theme
import resize from './mixins/resize'

const animationDuration = 6000

var xAxisData = ['软件开发', '图片租赁', '采购', '运输', '软件服务','运输费用','视频制作','动画制作','快递','制作'];
var firstData = [280, 52, 200, 334, 390, 330, 220,350,250,600];
var secondData = [80, 52, 200, 334, 390, 330, 220,200,350,380];
var lastData = [30, 52, 200, 334, 390, 330, 220,580,200,360]

export default {
  mixins: [resize],
  props: {
    className: {
      type: String,
      default: 'chart'
    },
    width: {
      type: String,
      default: '100%'
    },
    height: {
      type: String,
      default: '314px'
    }
  },
  data() {
    return {
      
      chart: null
    }
  },
  mounted() {
    this.$nextTick(() => {
      this.initChart()
    })
  },
  beforeDestroy() {
    if (!this.chart) {
      return
    }
    this.chart.dispose()
    this.chart = null
  },
  methods: {
    initChart() {
      this.chart = echarts.init(this.$el, 'macarons')

      this.chart.setOption({
        tooltip: {
          trigger: 'axis',
          axisPointer: { // 坐标轴指示器，坐标轴触发有效
            type: 'shadow' // 默认为直线，可选为：'line' | 'shadow'
          }
        },
        grid: {
          top: 10,
          left: '0%',
          right: '0%',
          bottom: '0%',
          containLabel: true
        },
        xAxis: [{
          type: 'category',
          data:xAxisData,
          axisTick: {
            alignWithLabel: true
          }
        }],
        yAxis: [{
          type: 'value',
          axisTick: {
            show: false
          }
        }],
        series: [{
          name: '预付款第一笔',
          type: 'bar',
          stack: 'vistors',
          barWidth: '60%',
          data: firstData,
          animationDuration
        }, {
          name: '预付款第二笔',
          type: 'bar',
          stack: 'vistors',
          barWidth: '60%',
          data: secondData,
          animationDuration
        }, {
          name: '尾款',
          type: 'bar',
          stack: 'vistors',
          barWidth: '60%',
          data: lastData,
          animationDuration
        }]
      })
    }
  }
}
</script>
