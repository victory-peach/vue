<template>
  <div class="form-container">
    <el-form
      :model="dynamicValidateForm"
      ref="dynamicValidateForm"
      label-width="100px"
      class="demo-dynamic"
    >
      <el-form-item prop="func1" label="函数表达式1">
        <el-input
          v-model="dynamicValidateForm.func1"
          class="input"
          placeholder="对数:Math.log() 指数:Math.pow(底数,x)"
        ></el-input>
      </el-form-item>
      <el-form-item prop="func2" label="函数表达式2">
        <el-input v-model="dynamicValidateForm.func2" class="input"></el-input>
      </el-form-item>
      <el-form-item prop="func3" label="函数表达式3">
        <el-input v-model="dynamicValidateForm.func3" class="input"></el-input>
      </el-form-item>
      <el-form-item>
        <el-button type="primary" @click="submitForm">提交</el-button>
        <el-button @click="resetForm('dynamicValidateForm')">重置</el-button>
      </el-form-item>
    </el-form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      dynamicValidateForm: {
        func1: "",
        func2: "",
        func3: "",
      },
    };
  },
  methods: {
    submitForm() {
      if (
        this.dynamicValidateForm.func1 ||
        this.dynamicValidateForm.func2 ||
        this.dynamicValidateForm.func3
      ) {
        this.$emit("formData", this.dynamicValidateForm);
      }
    },
    resetForm(formName) {
      this.$refs[formName].resetFields();
    },
    removeDomain(item) {
      var index = this.dynamicValidateForm.domains.indexOf(item);
      if (index !== -1) {
        this.dynamicValidateForm.domains.splice(index, 1);
      }
    },
    addDomain() {
      this.dynamicValidateForm.domains.push({
        value: "",
        key: Date.now(),
      });
    },
  },
};
</script>
<style lang="less" scoped>
.demo-dynamic {
  .input {
    width: 90%;
  }
  margin-top: 10px;
}
.form-container{
    border: 1px solid #EBEEF5;
    box-shadow: 0 2px 12px 0 rgba(0, 0 ,0 ,10%);
}
</style>