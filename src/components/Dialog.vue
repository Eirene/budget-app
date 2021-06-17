<template>
  <el-button type="text" @click="dialogVisible = true">click to open the Dialog</el-button>

  <el-dialog
      title="Confirm delete"
      v-model="dialogVisible"
      width="30%"
      :before-close="handleClose">
    <span>Are you sure?</span>
    <template #footer>
    <span class="dialog-footer">
      <el-button @click="dialogVisible = false">Cancel</el-button>
      <el-button type="danger" @click="dialogVisible = false">Delete</el-button>
    </span>
    </template>
  </el-dialog>
</template>

<script>
export default {
  data() {
    return {
      dialogVisible: false
    };
  },
  methods: {
    handleClose(done) {
      this.$confirm('Are you sure?')
          .then(() => {
            done();
            this.dialogVisible = false
          })
          .catch(() => {});
    }
  }
};
</script>
