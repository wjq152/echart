<template>
  <div :class="className" :style="{height:height,width:width}" />
</template>
<script>
import echarts from 'echarts'
require('echarts/theme/macarons') // echarts theme
import resize from './mixins/resize'
var clientlegendData = ['奥迪', '大众'];
var clientData = [100, 120, 161, 134, 105, 160, 165]
var clientData1 = [120, 82, 91, 154, 162, 140, 145]
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
      default: '350px'
    },
//     autoResize: {
//       type: Boolean,
//       default: true
//     },
//     chartData: {
//       type: Object,
//       required: true
//     }
  },
  data() {
    return {
      chart: null
    }
  },
//   watch: {
//     chartData: {
//       deep: true,
//       handler(val) {
//         this.setOptions(val)
//       }
//     }
//   },
  mounted() {
      this.initChart()
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
      this.chart = echarts.init(this.$el)
    //   this.charts.setOptions(){
    // setOptions() {
      this.chart.setOption({
        xAxis: {
          data: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun'],
          boundaryGap: false,
          axisTick: {
            show: false
          }
        },
        grid: {
          left: 10,
          right: 10,
          bottom: 20,
          top: 30,
          containLabel: true
        },
        tooltip: {
          trigger: 'axis',
          axisPointer: {
            type: 'cross'
          },
          padding: [5, 10]
        },
        yAxis: {
          axisTick: {
            show: false
          }
        },
        legend: {
          data: clientlegendData,
        },
        series: [{
          name: '奥迪',
          data: clientData,
          itemStyle: {
            normal: {
              color: '#FF005A',
              lineStyle: {
                color: '#FF005A',
                width: 2
              }
            }
          },
          smooth: true,
          type: 'line',
        //   data: expectedData,
          animationDuration: 2800,
          animationEasing: 'cubicInOut'
        },
        {
          name: '大众',
          data:clientData1,
          smooth: true,
          type: 'line',
          itemStyle: {         //折线图圆点样式
            normal: {
              color: '#3888fa',
              lineStyle: {
                color: '#3888fa',
                width: 2
              },
              areaStyle: {
                color: '#f3f8ff'
              }
            }
          },
        //   data: actualData,
          animationDuration: 2800,//动画延迟时间
          animationEasing: 'quadraticOut'//动画特效
        }]
      })
    }
  }
}
</script>
