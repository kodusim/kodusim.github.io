<style lang="less" scoped>
  .pie-chart-container {
    width: 100%;
    display: flex;
    flex-direction: column;
    align-items: center;
    .pie-labels {
      display: flex;
    }
    .label-group {
      display: flex;
      align-items: center;
    }
    .box {
      margin-right: 52px;
      &:last-child { margin-right: 0; }
    }
    .icon-box {
      width: 24px;
      height: 24px;
      display: flex;
      align-items: center;
      justify-content: center;
      margin-right: 6px;
    }
    .icon {
      width: 14px;
      height: 14px;
      border-radius: 100%;
      &.sp { background-color: #DCF2FF; }
      &.mp { background-color: #EAE0FF; }
      &.sm { background-color: #F2FFD6; }
      &.mm { background-color: #FFE8D3; }
    }
    .title {
      margin-right: 6px;
    }
  }
  .pie-chart {
    width: 128px;
    height: 128px;
    border-radius: 50%;
    margin-bottom: 20px;
  }
</style>
<template lang="pug">
  .pie-chart-container
    .pie-chart#mainChart
    .pie-labels
      .box
        .label-group
          .icon-box
            .icon.sp
          .title.Pretendard_body1_regular 태양인
          .label.Pretendard_body1_regular {{ sp }}%
        .label-group
          .icon-box
            .icon.sm
          .title.Pretendard_body1_regular 태음인
          .label.Pretendard_body1_regular {{ sm }}%
      .box
        .label-group
          .icon-box
            .icon.mp
          .title.Pretendard_body1_regular 소양인
          .label.Pretendard_body1_regular {{ mp }}%
        .label-group
          .icon-box
            .icon.mm
          .title.Pretendard_body1_regular 소음인
          .label.Pretendard_body1_regular {{ mm }}%
</template>
<script>
export default {
  props: {
    sp: {
      require: true,
    },
    sm: {
      require: true,
    },
    mp: {
      require: true,
    },
    mm: {
      require: true,
    },
  },
  mounted() {
    const chart = document.getElementById('mainChart');
    chart.style.background = `conic-gradient(#DCF2FF 0.00% ${this.sp}%, #EAE0FF ${this.sp}% ${this.sp + this.mp}%, #F2FFD6 ${this.sp + this.mp}% ${this.sp + this.mp + this.sm}%, #FFE8D3 ${this.sp + this.mp + this.sm}% ${this.sp + this.mp + this.sm + this.mm}%)`;
  },
};
</script>
