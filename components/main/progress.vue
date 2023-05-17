<style lang="less" scoped>
  .progress-wrapper {
    width: 100%;
    position: relative;
  }
  .progress-container {
    width: 100%;
    height: 8px;
    background-color: #D1EEC6;
    border-radius: 4px;
    position: relative;
    overflow: hidden;
    .progress-bar {
      position: absolute;
      left: 0;
      top: 0;
      height: 8px;
      background-color: #48E212;
      transition: .3s ease-in;
    }
  }
  .progress-label-box {
    transition: .3s ease-in;
    position: absolute;
    text-align: center;
    transform: translateX(-50%);
    .progress-arrow {
      position: absolute;
      top: 0;
      left: 50%;
      transform: translateX(-100%);
      width: 6px;
      height: 5px;
    }
    .progress-label {
      top: 5px;
      padding: 4px 10px;
      background-color: #48E212;
      border-radius: 44px;
      color: #ffffff;
      margin-top: 5px;
    }
  }
</style>
<template lang="pug">
  .progress-wrapper
    .progress-container
      .progress-bar(
        :style="{ width: widthValue }"
      )
    .progress-label-box(
      :style="{ left: widthValue }"
    )
      img.progress-arrow(src="./Vector 5.png")
      .progress-label.Gmarket_h5_bold {{ value }}/{{ max }}
</template>
<script>
export default {
  props: {
    max: {
      type: Number,
      default: 0,
    },
    value: {
      type: [Number, String],
      default: 0,
    },
  },
  computed: {
    widthValue() {
      if (this.max === 0) return 0;
      return `${(Number(this.value)/Number(this.max)) * 100}%`;
    },
  },
};
</script>
