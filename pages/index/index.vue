<style lang="less" scoped>
  .main-container {
    width: 100%;
    height: 100%;
    position: relative;
    box-sizing: border-box;
    overflow: hidden;
    .group {
      display: flex;
      position: absolute;
      left: 50%;
      transform: translateX(-50%);
      z-index: 0;
      &.image-box1 {
        top: 23px;
        align-items: flex-end;
      }
      &.image-box2 {
        bottom: 16px;
        align-items: flex-start;
      }
    }
    .image1 {
      width: 241px;
      height: 260px;
      margin-right: 24px;
    }
    .image2 {
      width: 227px;
      height: 255px;
    }
    .image3 {
      width: 238px;
      height: 218px;
      margin-right: 30px;
    }
    .image4 {
      width: 287px;
      height: 267px;
      margin-top: 16px;
    }
    .text-box {
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      z-index: 1;
      .title {
        margin-bottom: 12px;
      }
      .title, .label {
        text-align: center;
      }
    }
    .button-group {
      position: absolute;
      width: 100%;
      padding: 0 30px;
      bottom: 30px;
      z-index: 2;
      display: flex;
      align-items: center;
      .button {
        margin-right: 16px;
        &:last-child {
          margin-right: 0;
        }
      }
    }
  }
</style>
<template lang="pug">
  .main-container
    .group.image-box1
      img.image1(src="~/assets/image/illust-sun-boy.png")
      img.image2(src="~/assets/image/illust-moon-girl.png")
    .group.image-box2
      img.image3(src="~/assets/image/illust-small-boy.png")
      img.image4(src="~/assets/image/illust-small-girl.png")
    .text-box
      .title.Gmarket_h1_bold 체질별#[br]잎채소#[br]추천
      .label.Pretendard_body1_middle 동무 이제마 선생의#[br]사상체질 알아보기
    .button-group
      main-button.button(@click="$router.push('/test?type=simple')") 빠른검사
      main-button.button(@click="$router.push('/test?type=detail')") 정밀검사
</template>
