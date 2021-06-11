<template>
  <div>
    <el-row :gutter="20">
      <el-col :span="8" class="el">
        <div class="grid-content bg-purple"> 
          <Form @formData ="getForm" />
        </div>
          <Collapse @colData = "getcol"/>
      </el-col>
       <el-col :span="16">
        <div class="grid-content bg-purple">
          <Echarts :layout="funcData" :coltarget = "coltarget"/>
        </div>
      </el-col>
      
    </el-row>
  </div>
</template>

<script>
import Form from "@/views/components/Form.vue";
import Echarts from "@/views/components/Echarts.vue";
import Collapse from "@/views/components/Collapse.vue";
export default {
  data() {
    return {
      funcData: null,
      coltarget : null,
    };
  },
  components: {
    Form,
    Echarts,
    Collapse
  },
  methods: {
    getForm(val) {
      // console.log(val);
      // console.log(val);
      this.funcData = val;
    },
    getcol(val){
      this.coltarget = val;
    }
  },
};
</script>

<style lang="less">
.el-row {
  margin-bottom: 20px;
  &:last-child {
    margin-bottom: 0;
  }
}
.el-col {
  border-radius: 4px;
}
.el{
  padding-left: 30px !important;
  box-sizing: border-box;
}
// .bg-purple-dark {
//   background: #99a9bf;
// }
// .bg-purple {
//   background: #d3dce6;
// }
// .bg-purple-light {
//   background: #e5e9f2;
// }
.grid-content {
  border-radius: 4px;
  min-height: 36px;

}
.row-bg {
  padding: 10px 0;
  background-color: #f9fafc;
}
.echarts-content{
  width: 1000px;
  height: 680px;
}
.form-container{
  margin-top: 30px;
  margin-bottom: 40px;
}
</style>