<!-- src/components/SelectQuestion.vue -->
<template>
  <form class="select-question" @submit.prevent="handleSubmit">
    <dl>
      <dt>{{message}}</dt>
      <dd>
        <template v-for="(choice, i) in choices">
          <label>
            <input type="radio" :value="i+1" :key="choice" v-model="selectedValue">
            {{choice}}
            <br>
          </label>
        </template>
      </dd>
    </dl>
    <button>次へ</button>
  </form>
</template>

<script>
export default {
  props: {
    message: String,
    choices: Array,
    value: Number
  },
  data() {
    return {
      selectedValue: this.value
    };
  },
  methods: {
    handleSubmit() {
      this.$emit("input", this.selectedValue);
      this.$emit("next");
    }
  },
  created() {
    this.selectedValue = 1;
  }
};
</script>

<style scoped>
</style>