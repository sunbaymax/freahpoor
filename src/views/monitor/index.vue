<!--  -->
<template>
  <div class="app-container">
    <el-breadcrumb separator-class="el-icon-arrow-right">
      <el-breadcrumb-item :to="{ path: '/monitor' }">实时监控</el-breadcrumb-item>
      <el-breadcrumb-item></el-breadcrumb-item>
    </el-breadcrumb>
    <div class="topitem">
      <!-- <h4>选项卡展示</h4> -->
      <data-tabs :option="easyDataOption"></data-tabs>
    </div>
    <div class="itemcenter" :gutter="20">
      <el-tabs tab-position="left">
        <el-tab-pane class="a1" label="#A5">
          <el-row>
            <el-col :span="6" v-for="(item,index) in 40" :key="index">
              <div class="itemone" @click="handlestore">
                <div class="storename">商铺101</div>
                <div class="storeshebei">PLC{{index+1}}</div>
                
                  <img  class="state" src="@/assets/images/img/normalsign.png" alt="">
                
              </div>
            </el-col>
          </el-row>
        </el-tab-pane>
        <el-tab-pane label="#B1">1</el-tab-pane>
        <el-tab-pane label="#B2">2</el-tab-pane>
        <el-tab-pane label="#B3">3</el-tab-pane>
        <el-tab-pane label="#B4">4</el-tab-pane>
        <el-tab-pane label="#B5">5</el-tab-pane>
      </el-tabs>
    </div>
  </div>
</template>

<script>
//这里可以导入其他文件（比如：组件，工具js，第三方插件js，json文件，图片文件等等）
//例如：import 《组件名称》 from '《组件路径》';
import DataDisplay from "@/components/data-display/data-display.vue";
import DataTabs from "@/components/data-tabs/data-tabs.vue";

export default {
  //import引入的组件需要注入到对象中才能使用
  components: { DataDisplay, DataTabs },
  data() {
    //这里存放数据
    return {
      arr: [1, 2, 3, 4, 5, 6, 7, 8],
      easyDataOption: {
        span: 8,
        gutter: 0,
        data: [
          {
            title: "正常运行",
            subtitle: "",
            count: 20,
            allcount: 2000,
            text: "当前记录数",
            color:
              "url(" +
              require("../../assets/images/img/zhengchangbg.png") +
              ")",
            key: ""
          },
          {
            title: "状态异常",
            subtitle: "",
            count: 3112,
            allcount: 10222,
            text: "当前故障数",
            color:
              "url(" + require("../../assets/images/img/yichangbg.png") + ")",
            key: "故"
          },
          {
            title: "掉线",
            subtitle: "",
            count: 908,
            allcount: 10222,
            text: "评论次数",
            color:
              "url(" + require("../../assets/images/img/diaoxianbg.png") + ")",
            key: "评"
          }
        ]
      },
      obj: {},
      gettime: "", //当前时间
      getcity: "", //当前城市
      getIp: "",
      getweatherifo: {}
    };
  },
  //监听属性 类似于data概念
  computed: {},
  //监控data中的数据变化
  watch: {},
  //方法集合
  methods: {
    handlestore(){
      let id=10001;
      this.$router.push({
          path: `/storeinfo/${id}`,
        })
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
<style >
.topitem .el-tabs--left .el-tabs__item .is-left {
    text-align: center!important;
}
.itemcenter .el-tabs__item {
 
  height: 100px;
  width: 74px;
  line-height: 100px;
  display: flex;
  justify-content: center;
  align-items: center;
  background: #fff;
  border-bottom: 1px solid #e8e8e8;
  font-weight: bold;
  border-radius: 5px;
  font-size: 20px;
}
</style>
<style scoped>
.itemone {
  background: url('../../assets/images/img/storebg.png') no-repeat;
  background-size:contain;
  height: 170px;
  width: 320px;
  margin-bottom: 15px;
  padding: 20px;
  box-sizing: border-box;
  position: relative;
  border-radius: 5px;
 
}
.itemone .storename{
  
  height: 30px;
  line-height: 30px;
  color:#0E64FE;
  font-size: 25px;
}
.itemone .storeshebei{
  height: 26px;
  line-height: 26px;
  color:#999999;
  font-size: 16px;
}
.itemone .state{
  display: inline-block;
  width: 30px;
  height: 30px;
  position: absolute;
  bottom: 14px;
  right: 14px;
}
.topitem .el-col-8 .item {
  position: relative;
  margin: 15px;
  padding: 12px;
  height: 174px;
  width: 60% !important;
  border-radius: 4px;
  box-sizing: border-box;
  overflow: hidden;
  color: #fff;
  border: 1px solid #555555;
}

.title {
  padding: 15px 10px;
  box-sizing: border-box;
  background: #fff;
  border-radius: 5px;
}
.user-info {
  display: flex;
  align-items: center;
  /* padding-bottom: 20px;
  border-bottom: 2px solid #ccc; */
  margin-bottom: 15px;
}
.user-info-role {
  padding-left: 3px;
}
.user-info-list {
  padding: 15px;
}
.user-avator {
  width: 120px;
  height: 120px;
  border-radius: 50%;
}

.user-info-cont {
  padding-left: 50px;
  flex: 1;
  font-size: 14px;
  color: #999;
}

.user-info-cont div:first-child {
  font-size: 30px;
  color: #222;
}

.user-info-list {
  display: flex;
  /* justify-content: space-between; */
  font-size: 14px;
  color: #999;
  line-height: 25px;
}
.user-info-list p {
  margin: 0 10px 0 5px;
}
.user-info-list span {
  margin-left: 0 10px 0 0;
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
</style>


