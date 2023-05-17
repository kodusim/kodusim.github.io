<style lang="less" scoped>
  .test-container {
    width: 100%;
    height: 100%;
    padding-top: 52px;
    padding-bottom: 86px;
    .contents {
      width: 100%;
      height: 100%;
      padding: 30px;
      overflow: auto;
      .progress {
        margin-bottom: 60px;
      }
      .question {
        margin-bottom: 30px;
      }
    }
    .button-box {
      position: fixed;
      width: 100%;
      max-width: 500px;
      padding: 0 30px;
      bottom: calc(env(safe-area-inset-bottom) + 30px);
    }
  }
</style>
<template lang="pug">
  .test-container
    test-header(
      @back="$router.go(-1)"
    )
    .contents
      main-progress.progress(
        :max="qDatas.length"
        :value="nowIdx + 1"
      )
      test-question.question(
        :idx="nowIdx"
        :question="nowData.question"
      )
      test-select(
        :value.sync="selectAnswer"
        :data="nowData.answer"
      )
    .button-box
      main-button(
        @click="next"
      ) {{ nextLabel }}
</template>
<script>
import Question from '~/assets/json/Question.json'
import TestHeader from './.components/TestHeader';
import TestQuestion from './.components/TestQuestion';
import TestSelect from './.components/TestSelect';

export default {
  asyncData({ query }) {
    const q = query.type;
    let qDatas = [];
    if (q === 'simple') {
      qDatas = Question.slice(0, 15);
    } else {
      qDatas = Question;
    }
    return { qDatas };
  },
  mounted() {
    this.nowIdx = 0;
  },
  watch: {
    nowIdx(val) {
      this.nowData = this.qDatas[val];
    },
  },
  computed: {
    nextLabel() {
      if (this.nowIdx === this.qDatas.length - 1) return '완료';
      return '다음';
    },
  },
  components: { TestHeader, TestQuestion, TestSelect },
  data() {
    return {
      nowData: {},
      selectAnswer: -1,
      isLoading: true,
      nowIdx: -1,
      answerDatas: [],
    };
  },
  methods: {
    async next() {
      if (this.selectAnswer < 0) {
        this.$message.error('선택항목을 선택해주세요');
        return;
      }
      this.answerDatas.push(this.selectAnswer + 1);
      if (this.qDatas.length - 1 === this.nowIdx) {
        await this.postTest();
        return;
      }
      this.nowIdx += 1;
      this.selectAnswer = -1;
    },
    async postTest() {
      try {
        const { data: testData } = await this.$axios.post('/user/sieving-test', {
          testData: this.answerDatas,
        });
        this.$cookies.set('result', testData);
        this.$router.push('/result');
      } catch (e) {
        console.log(e);
      }
    },
  },
};
</script>
