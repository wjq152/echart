<template>
  <div :class="className" :style="{height:height,width:width}" />
</template>
<script>
import echarts from 'echarts'
require('echarts/theme/macarons') // echarts theme
import resize from './mixins/resize'
var legendData = ['软件开发', '图片租赁', '采购', '运输', '软件服务','运输费用','视频制作','动画制作','快递','制作'];
var pieData =  [
              { value: 25000, name: '软件开发' },
              { value: 25000, name: '图片租赁' },
              { value: 180000, name: '采购' },
              { value: 250, name: '运输' },
              { value: 4759, name: '软件服务' },
              { value: 138, name: '运输费用' },
              { value: 27000, name: '视频制作' },
              { value: 40200, name: '动画制作' },
              { value: 23, name: '快递' },
              { value: 12325, name: '制作' },
            ];
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
      chart: null, 
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
          trigger: 'item',
          formatter: '{a} <br/>{b} : {c} ({d}%)'
        },
        legend: {
          left: 'center',
          bottom: '10',
          data: legendData,
        },
        series: [
          {
            name: '合同总金额',
            type: 'pie',
            roseType: 'radius',
            radius: [15, 95],
            center: ['50%', '38%'],
            data: pieData,
            animationEasing: 'cubicInOut',
            animationDuration: 2600
          }
        ]
      })
    }
  }
}
</script>
