<template>
  <div>
    <a href="#" @click="selectSex" v-model="sex" value="0">女性から男性用</a>
    <br>
    <a href="#" @click="selectSex" v-model="sex" value="1">男性から女性用</a>
    <br>
  </div>
</template>

<script>
export default {
  data() {
    return {
      sex: 0
    };
  },
  methods: {
    selectSex: this.value
  }
};
</script>

<style scoped>
</style>