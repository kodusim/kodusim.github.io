<style lang="less" scoped>
  .result-container {
    width: 100%;
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 40px 30px 116px 30px;
    .status {
      margin: 28px;
    }
    .image, .sieving, .analysis, .point {
      margin-bottom: 30px;
    }
    .button-container {
      width: 100%;
      max-width: 500px;
      position: fixed;
      padding: 30px;
      bottom: env(safe-area-inset-bottom);
    }
  }
</style>
<template lang="pug">
  .result-container
    result-status.status(
      :class="checkSieving"
    ) 검사결과
    result-image.image(
      :value="checkSieving"
    )
    result-sieving.sieving(
      :value="checkSieving"
    )
    result-analysis.analysis(
      :sieving="result.sieving"
    )
    result-point.point(
      :value="checkSieving"
    )
    result-plants.plants(
      :plants="result.recommendedSalad"
    )
    .button-container
      main-button(@click="applicationVisible = true") 샐러드 신청하기
    application-dialog(
      :visible="applicationVisible"
      :name.sync="applicationName"
      @cancel="applicationVisible = false"
      @submit="order"
    )
    success-dialog(
      :visible="isSubmit"
      :name="applicationName"
      @submit="success"
    )
</template>
<script>
import _ from 'lodash';
import ResultStatus from './.components/ResultStatus';
import ResultImage from './.components/ResultImage';
import ResultSieving from './.components/ResultSieving';
import ResultAnalysis from './.components/ResultAnalysis';
import ResultPoint from './.components/ResultPoint';
import ResultPlants from './.components/ResultPlants';
import ApplicationDialog from './.components/ApplicationDialog';
import SuccessDialog from './.components/SuccessDialog';

export default {
  asyncData({ $cookies }) {
    const result = $cookies.get('result');
    return { result };
  },
  components: { ResultStatus, ResultImage, ResultSieving, ResultAnalysis, ResultPoint, ResultPlants, ApplicationDialog, SuccessDialog },
  computed: {
    checkSieving() {
      const { soeumin, soyangin, taeeumin, taeyangin } = this.result.sieving;
      const max = Math.max(soeumin, soyangin, taeeumin, taeyangin);
      if (soeumin === max) return 'mm';
      if (soyangin === max) return 'mp';
      if (taeeumin === max) return 'sm';
      if (taeyangin === max) return 'sp';
      return '';
    },
  },
  watch: {
    applicationVisible(val) {
      if (!val) {
        if (!this.isSubmit) this.applicationName = '';
      }
    },
  },
  data() {
    return {
      applicationName: '',
      isSubmit: false,
      applicationVisible: false,
    };
  },
  methods: {
    success() {
      this.$router.push('/');
    },
    async order() {
      if (!this.applicationName) {
        this.$message('이름을 입력해주세요');
        return;
      }
      try {
        await this.$axios.post('/user/orders/salad', {
          userName: this.applicationName,
          ...this.result,
        })
        this.isSubmit = true;
        this.applicationVisible = false;
      } catch (e) {
        console.log(e);
      }
    },
  },
};
</script>
