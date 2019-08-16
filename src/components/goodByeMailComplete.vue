<template>
  <div>
    <h2>完成</h2>
    <p>これで別れの手紙ができました。カジュアルに修羅場に突入しましょう。この手紙を送ったことによって生じる被害についてはイッツ・コミュニケーションズ株式会社は一切関知しません。</p>
    <a href="#" v-on:click="$emit('reset')">気にいらないからやり直す</a>
    <br>
    <p>
      <input type="text" readonly :value="shareUrl">
      <a target="_blank" :href="twitterUrl">つぶやく</a>
    </p>
  </div>
</template>

<script>
import { stringify } from "querystring";

export default {
  props: {
    questions: Object,
    step: Number
  },
  computed: {
    shareUrl() {
      const shareData = {
        ...this.questions.target,
        ...this.questions,
        target: null,
        share: 1
      };
      delete shareData.target;
      return `https://dailyportalz.jp/kiji/wakareno-tegami-generator?${stringify(
        shareData
      )}`;
    },
    twitterUrl() {
      return `https://twitter.com/intent/tweet?text=別れの手紙ジェネレーター&url=${encodeURIComponent(
        this.shareUrl
      )}`;
    }
  },
  methods: {
    handleClickRestart() {
      location.href = location.href.replace(location.search, "");
    }
  }
};
</script>

<style scoped>
</style>