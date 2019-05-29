<template>
  <div class="dashboard-editor-container">
    <el-row  style="background: #fff;
    padding: 16px  0 16px 0;
    margin-bottom: 32px;">
      <el-col>
        <div id='select' class="datatable-select">
          <el-select v-model="value" filterable placeholder="请选择" @change="changeChart">
          <el-option
            v-for="item in options"
            :key="item.value"
            :label="item.label"
            :value="item.value">
            </el-option>
        </el-select>
        </div>
        
      </el-col>
    </el-row>
   
    <el-row :gutter="32">
        <el-col :xs="24" :sm="24" :lg="12">
        <div id="pie" class="chart-wrapper">
          <pie-chart />
        </div>
      </el-col>
      <el-col :xs="24" :sm="24" :lg="12">
        <div id="bar" class="chart-wrapper">
          <bar-chart />
        </div>
      </el-col>
    </el-row>
    <el-row style="background:#fff;padding:16px 16px 0;margin-bottom:32px;">
        <div><line-chart/>
        </div>
    </el-row>
  </div>
</template>

<script>


import LineChart from './components/LineChart'


import PieChart from './components/PieChart'
import BarChart from './components/BarChart'

var chartArr1 = [document.getElementById('pie'),document.getElementById('bar')]
var chartArr2 = [document.getElementById('pie'),document.getElementById('bar')]

export default {
  name: 'DashboardAdmin',
  components: {
    LineChart,
    PieChart,
    BarChart,
  },
  data() {
    return {
       options: [{
          value: '1',
          label: '项目一'
        }, {
          value: '2',
          label: '项目二'
        }, {
          value: '3',
          label: '项目三'
        }, {
          value: '4',
          label: '项目四'
        }, {
          value: '5',
          label: '项目五'
        }],
        value:'',
        
    }
  },
  methods: {
      changeChart :  
       function (val) {
            let that = this;
            that.value=val.value;//获取value
             console.log(val)
      },
     
  }
}

</script>

<style lang="scss" scoped>
.dashboard-editor-container {
  padding: 32px;
  background-color: rgb(240, 242, 245);
  position: relative;

  .github-corner {
    position: absolute;
    top: 0px;
    border: 0;
    right: 0;
  }

  .chart-wrapper {
    background: #fff;
    padding: 16px 16px 0;
    margin-bottom: 32px;
  }
}

@media (max-width:1024px) {
  .chart-wrapper {
    padding: 8px;
  }
}
</style>
