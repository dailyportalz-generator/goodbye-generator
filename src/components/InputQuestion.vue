<!-- src/components/InputQuestion.vue -->
<template>
  <form class="input-question" @submit.prevent="handleSubmit">
    <dl>
      <dt>まず、相手の名前と敬称を入れてください。</dt>
      <dd>
        <input type="text" v-model="name" required>
        <select v-model="title" required>
          <option :value="1">さま</option>
          <option :value="2">様</option>
          <option :value="3">殿</option>
          <option :value="4">さん</option>
          <option :value="5">くん</option>
          <option :value="6">ちゃん</option>
        </select>
      </dd>
    </dl>
    <button>次へ</button>
  </form>
</template>

<script>
import { METHODS } from "http";
export default {
  data() {
    return {
      name: "",
      title: 1
    };
  },
  methods: {
    handleSubmit() {
      this.$emit("start", {
        name: this.name,
        title: this.title
      });
    }
  }
};
</script>

<style scoped>
</style>