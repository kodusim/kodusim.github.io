<style lang="less">
  .main-el-dialog {
    display: flex;
    align-items: center;
    justify-content: center;
    .el-dialog {
      width: 332px;
      background-color: transparent;
      box-shadow: none;
      margin-top: 0 !important;
    }
    .el-dialog__header {
      display: none;
    }
    .el-dialog__body {
      width: 332px;
      padding: 30px;
      background-color: #FFFFFF;
      box-shadow: 0px 10px 30px rgba(0, 0, 0, 0.1);
      border-radius: 30px;
    }
  }
</style>
<template lang="pug">
  el-dialog.main-el-dialog(
    :visible="visible"
  )
    slot
</template>
<script>
export default {
  props: {
    visible: {
      type: Boolean,
      default: false,
    },
  },
};
</script>
