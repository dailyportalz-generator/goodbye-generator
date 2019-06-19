<!-- dailyportal@itscom.jp -->

<template>
  <div id="app">
    <template>
      <div v-if="step === 0">
        <a href="#" @click.prevent="selectSex(0)">女性から男性用</a>
        <br>
        <a href="#" @click.prevent="selectSex(1)">男性から女性用</a>
        <br>
      </div>

      <span v-if="step > 0 && step < 8">
        <b>step{{step}}</b>
      </span>
      <InputQuestion key="start" v-if="step === 1" @start="handleStart"/>

      <SelectQuestion
        key="question1"
        v-if="step === 2"
        v-model="questions.q1"
        @next="handleNext"
        :message="messageList[0]"
        :choices="choicesList[0]"
      />

      <SelectQuestion
        key="question2"
        v-if="step === 3"
        v-model="questions.q2"
        @next="handleNext"
        :message="messageList[1]"
        :choices="choicesList[1]"
      />

      <SelectQuestion
        key="question3"
        v-if="step === 4"
        v-model="questions.q3"
        @next="handleNext"
        :message="messageList[2]"
        :choices="choicesList[2]"
      />

      <SelectQuestion
        key="question4"
        v-if="step === 5"
        v-model="questions.q4"
        @next="handleNext"
        :message="messageList[3]"
        :choices="choicesList[3]"
      />

      <SelectQuestion
        key="question5"
        v-if="step === 6"
        v-model="questions.q5"
        @next="handleNext"
        :message="messageList[4]"
        :choices="choicesList[4]"
      />

      <SelectQuestion
        key="question6"
        v-if="step === 7"
        v-model="questions.q6"
        @next="handleNext"
        :message="messageList[5]"
        :choices="choicesList[5]"
      />
      <goodByeMailComplete
        v-if="step === 8"
        :step="step"
        :questions="questions"
        @reset="step = 0;
        questions.name = '';
        questions.title = 1;
        questions.sex = 0;
        questions.q1 = 0;
        questions.q2 = 0;
        questions.q3 = 0;
        questions.q4 = 0;
        questions.q5 = 0;
        questions.q6 = 0;
        
        "
      />
      <goodByeMailResult v-if="step !== 0" :step="step" :questions="questions"/>
    </template>
  </div>
</template>

<script>
import goodByeMailComplete from "./components/goodByeMailComplete.vue";
import goodByeMailResult from "./components/goodByeMailResult.vue";
import InputQuestion from "./components/InputQuestion.vue";
import SelectQuestion from "./components/SelectQuestion.vue";
import { parse } from "querystring";

export default {
  name: "app",
  data() {
    return {
      step: 0,
      questions: {
        name: "",
        title: 1,
        sex: 0,

        q1: 0,
        q2: 0,
        q3: 0,
        q4: 0,
        q5: 0,
        q6: 0
      }
    };
  },
  components: {
    InputQuestion,
    SelectQuestion,
    goodByeMailResult,
    goodByeMailComplete
  },
  mounted() {
    const params = parse(location.search.replace("?", ""));
    const isValid = ["name", "title", "q1", "q2", "q3", "q4", "q5", "q6"].every(
      val => {
        if (!params[val]) {
          return false;
        }
        if (val != "name" && parseInt(params[val]) < 1) {
          return false;
        }
        return true;
      }
    );
    if (isValid) {
      const questions = {
        name: params.name,
        title: parseInt(params.title),
        q1: parseInt(params.q1),
        q2: parseInt(params.q2),
        q3: parseInt(params.q3),
        q4: parseInt(params.q4),
        q5: parseInt(params.q5),
        q6: parseInt(params.q6)
      };
      this.questions = questions;
      this.step = 7;
    }
  },
  methods: {
    selectSex(value) {
      this.questions.sex = value;
      this.handleNext();
    },
    handleNext() {
      this.step++;
    },
    handleStart(startData) {
      this.questions.name = startData.name;
      this.questions.title = startData.title;
      this.handleNext();
    }
  },
  computed: {
    messageList() {
      if (this.questions.sex == 0) {
        return [
          "書き出しは",
          "そろそろ別れ話を匂わせます",
          "切り出します",
          "なんで別れるの？",
          "貸してた本はどうする？",
          "しめは？"
        ];
      } else {
        return [
          "書き出しは",
          "相手とのおつきあいの期間は",
          "では本題に",
          "なんで別れるの？",
          "貸してたCDはどうする？",
          "しめは？"
        ];
      }
    },
    choicesList() {
      if (this.questions.sex == 0) {
        return [
          [
            "普通な感じで",
            "まさか別れとは思わせずに",
            "季節の話題で",
            "不吉な予感を感じさせつつ"
          ],
          [
            "深刻な感じで",
            "学校の先生みたいに",
            "乙女ちっくに",
            "不吉な予感はいっそう高まる"
          ],
          [
            "ストレートに",
            "やややんわりと",
            "ありがちに正直に",
            "言いにくいから外国人風に"
          ],
          [
            "相手のしぐさが",
            "自分のせいにして",
            "立ち直れないように",
            "うそついて"
          ],
          [
            "どうでもいい",
            "ロマンチックに",
            "返せ",
            "さらに立ち直れないように"
          ],
          [
            "ふつうに",
            "自分がいい人みたいに",
            "完全に切るのはもったいないかな",
            "立ち直れない最後のセリフ"
          ]
        ];
      } else {
        return [
          [
            "いつもどおりに",
            "ラブラブに",
            "詩人のように",
            "事件を感じさせる書き出し"
          ],
          ["１年以上", "１年未満", "１週間ぐらい", "つきあってない"],
          ["ストレートに", "遠まわしに", "マッキーみたいに", "うそで固めて"],
          [
            "なんかわかんないけどかっこよさげに",
            "スター気どりで",
            "くだらない理由で",
            "マニアックに"
          ],
          [
            "どうでもいい",
            "詩人のように",
            "微妙なんだよなー",
            "イヤミをまじえて"
          ],
          ["ふつうに", "ダ○ンプのように", "弱っちく", "ばかにして"]
        ];
      }
    }
  }
};
</script>

<style>
</style>