<!--  -->
<template>
  <div class="app-container">
    <el-breadcrumb separator-class="el-icon-arrow-right">
      <el-breadcrumb-item :to="{ path: '/monitor' }">实时监控</el-breadcrumb-item>
      <el-breadcrumb-item>养殖池监控</el-breadcrumb-item>
    </el-breadcrumb>
    <div class="tabledata">
      <el-row>
        <el-col :xs="24" :sm="24" :md="24" :lg="24" :xl="24">
          <el-table
            :data="tableData"
            style="width: 100%"
            :cell-style="rowClass"
            :header-cell-style="headClass"
          >
            <el-table-column label="养殖池编号">
              <template slot-scope="scope">
                <span v-bind:class="[{'redwen':scope.row.idnum%2 ==0},circle]">{{ scope.row.idnum }}</span>
              </template>
            </el-table-column>
            <el-table-column label="温度">
              <template slot-scope="scope">
                <span
                  v-bind:class="[{'redwen':scope.row.temperature>30}]"
                >{{ scope.row.temperature }}</span>
              </template>
            </el-table-column>
            <el-table-column prop="model" label="模式"></el-table-column>
            <el-table-column prop="flow" label="水流"></el-table-column>
            <el-table-column prop="state" label="状态"></el-table-column>
          </el-table>
        </el-col>
      </el-row>
    </div>
    <div class="mychoose">
      <p style="color:#0E64FE">单位：摄氏度℃</p>
      <p>
        7天温度变化折线
        <el-select v-model="chizi" >
          <el-option label="1号养殖池" value="1号养殖池"></el-option>
          <el-option label="2号养殖池" value="2号养殖池"></el-option>
        </el-select>
      </p>
    </div>
    <div class="dataline">
      <el-row>
        <el-col :xs="24" :sm="24" :md="24" :lg="24" :xl="24">
          <div class="chart_box">
            <ve-line :data="chartData" :settings="chartSettings"></ve-line>
          </div>
        </el-col>
      </el-row>
    </div>
  </div>
</template>

<script>
export default {
  //import引入的组件需要注入到对象中才能使用
  data() {
    this.chartSettings = {
      metrics: ["温度"],
      dimension: ["日期"],
      area: true,
      itemStyle: {
        //面积图颜色设置
        color: {
          type: "linear",
          x: 0,
          y: 0,
          x2: 0,
          y2: 1,
          colorStops: [
            {
              offset: 0,
              color: "rgba(53,116,220,0.6)" // 0% 处的颜色
            },
            {
              offset: 1,
              color: "rgba(53,116,220,0.1)" // 100% 处的颜色
            }
          ],
          globalCoord: false // 缺省为 false
        }
      }
    };
    //这里存放数据
    return {
      chizi: "1号养殖池",
      chartData: {
        columns: ["日期", "温度"],
        rows: [
          { 日期: "2020-3-25", 温度: 23.5 },
          { 日期: "2020-3-26", 温度: 22.1 },
          { 日期: "2020-3-27", 温度: 16.8 },
          { 日期: "2020-3-28", 温度: 24.6 },
          { 日期: "2020-3-29", 温度: 30.5 },
          { 日期: "2020-3-30", 温度: 27.6 }
        ]
      },
      circle: "circle",
      tableData: [
        {
          idnum: 1,
          temperature: "25.3",
          model: "自动",
          flow: "开启",
          state: "制冷"
        },
        {
          idnum: 2,
          temperature: "30.6",
          model: "自动",
          flow: "开启",
          state: "制冷"
        },
        {
          idnum: 3,
          temperature: "21.6",
          model: "自动",
          flow: "关闭",
          state: "制冷"
        },
        {
          idnum: 4,
          temperature: "28.6",
          model: "自动",
          flow: "关闭",
          state: "制热"
        },
        {
          idnum: 5,
          temperature: "25.6",
          model: "自动",
          flow: "关闭",
          state: "制冷"
        }
      ]
    };
  },
  //监听属性 类似于data概念
  computed: {},
  //监控data中的数据变化
  watch: {},
  //方法集合
  methods: {
    // 表头样式设置
    headClass() {
      return "text-align: center;color:#0E64FE;font-size:15px;";
    },
    // 表格样式设置
    rowClass() {
      return "text-align: center;font-size:14px;";
    }
  },
  //生命周期 - 创建完成（可以访问当前this实例）
  created() {
    this.obj = JSON.parse(sessionStorage.getItem("user"));
    console.log(this.obj);
  },
  //生命周期 - 挂载完成（可以访问DOM元素）
  mounted() {},
  //生命周期 - 创建之前
  beforeCreate() {},
  //生命周期 - 挂载之前
  beforeMount() {},
  //生命周期 - 更新之前
  beforeUpdate() {},
  //生命周期 - 更新之后
  updated() {},
  //生命周期 - 销毁之前
  beforeDestroy() {},
  //生命周期 - 销毁完成
  destroyed() {},
  //如果页面有keep-alive缓存功能，这个函数会触发
  activated() {}
};
</script>
<style>
.tabledata .el-table .cell {
  line-height: inherit;
}
.mychoose .el-select {
  background: none;
  margin-left: 15px;
}
.mychoose .el-select .el-input__inner{
  background: none;
  font-size: 14px;
}
</style>
<style scoped>
.mychoose{
   margin: 15px 0;
    font-size: 15px;
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.dataline {
  margin: 15px 0;
}
.tabledata {
  /* padding: 15px 10px; */
  box-sizing: border-box;
  background: #fff;
  border-radius: 5px;
}
.tabledata li {
  list-style-type: none;
}
.tabledata .circle {
  display: inline-block;
  text-align: center;
  width: 20px;
  height: 20px;
  border: 1px solid grey;
  border-radius: 50%;
  font-size: 14px;
}

.redwen {
  color: #ea6472;
}
.greenwen {
  color: #4fd992;
}
/* @import url(); 引入公共css类 */
.app-container {
  background-color: #fcf9fc;
}
.item {
  margin-bottom: 16px;
}
.item h4 {
  font-size: 16px;
  font-weight: bold;
  line-height: 1.15;
  padding: 15px 0 15px 0px;
}
.chart_box{
  height: 500px;
}
</style>