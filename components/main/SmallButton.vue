<style lang="less" scoped>
  .main-button-container {
    width: 100%;
    height: 56px;
    background-color: #48E212;
    border-radius: 16px;
    display: flex;
    align-items: center;
    justify-content: center;
    cursor: pointer;
    color: #ffffff;
  }
</style>
<template lang="pug">
  .main-button-container.Gmarket_body1_bold1(
    @click="$emit('click')"
  )
    slot
</template>
