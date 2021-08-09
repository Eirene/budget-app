<template>
  <el-card class="form-card">
    <el-form :model="formData" ref="addItemForm" :rules="rules" lable-position="top">
      <el-form-item label="Type" prop="type">
        <el-select class="type-select" v-model="formData.type" placeholder="Choose type...">
          <el-option lable="Income" value="Income"/>
          <el-option lable="Outcome" value="Outcome"/>
        </el-select>
      </el-form-item>
      <el-form-item label="Comments" prop="comment">
        <el-input v-model="formData.comment"/>
      </el-form-item>
      <el-form-item label="Value" prop="value">
        <el-input v-model.number="formData.value"/>
      </el-form-item>
      <el-button @click="onSubmit" type="primary">Submit</el-button>
    </el-form>
  </el-card>
</template>

<script>
export default {
  name: "Form",
  data: () => {
    const checkAmount = (rule, value, callback) => {
      if (!value) {
        return callback(new Error('Please input the amount'));
      }
      return callback();
    };
    return {
      formData: {
        type: "Outcome",
        comment: "",
        value: 0
      },
      rules: {
        type: [
          {required: true, message: "Please select type", trigger: "blur"}
        ],
        comment: [
          {required: true, message: "Please input comment", trigger: "change"}
        ],
        value: [
          {required: true, message: "Please input value", trigger: "change"},
          {type: "number", message: "Value must be a number", trigger: "change"},
          {validator: checkAmount, message: "Should be positive or negative amount"}
        ]
      }
    }
  },
  methods: {
    onSubmit() {
      this.$refs.addItemForm.validate(valid => {
        if (valid) {
          if (this.formData.type === 'Outcome') {
            this.formData.value = -this.formData.value
          }
          this.$emit("submitForm", {...this.formData});
          this.$refs.addItemForm.resetFields();
        }
      });
    },
  }
};
</script>

<style scoped>
.form-card {
  margin-top: 73px;
}
.type-select {
  width: 100%;
}
</style>
