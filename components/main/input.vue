<style lang="less" scoped>
  .main-input {
    width: 100%;
    padding: 14px 16px;
    height: 52px;
    background-color: #FFFFFF;
    border: 1px solid #D8D8D8;
    border-radius: 8px;
  }
</style>
<template lang="pug">
  input.main-input(
    :value="value"
    @input="$emit('input', $event.target.value)"
    :placeholder="placeholder"
  )
</template>
<script>
export default {
  props: {
    value: {
      type: String,
      default: '',
    },
    placeholder: {
      type: String,
      default: '',
    },
  },
};
</script>
