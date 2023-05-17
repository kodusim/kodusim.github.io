<style lang="less" scoped>
  .main-check-box-container {
    display: flex;
    align-items: flex-start;
    cursor: pointer;
    .icon {
      width: 24px;
      height: 24px;
      margin-right: 10px;
    }
  }
</style>
<template lang="pug">
  .main-check-box-container(
    @click="send"
  )
    img.icon(v-if="isCheck" src="~/assets/icon/icon-checkbox-filled.png")
    img.icon(v-else src="~/assets/icon/icon-checkbox-empty.png")
    .label.Pretendard_body1_regular
      slot
</template>
<script>
export default {
  props: {
    value: { require: true },
    radio: {
      type: Boolean,
      default: false,
    },
    data: { require: true },
  },
  computed: {
    isCheck() {
      if (this.radio) {
        if (this.value === this.data) return true;
        return false;
      } else {
        if (this.value) return true;
        return false;
      }
    },
  },
  methods: {
    send() {
      if (this.radio) {
        this.$emit('input', this.data);
      } else {
        this.$emit('input', !this.value);
      }
    },
  },
};
</script>
