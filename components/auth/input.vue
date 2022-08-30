<script setup lang="ts">
  const props = defineProps(["modelValue"])
  const model = useVModel(props,"modelValue")
</script>
<template>
  <input v-model="model"/>
</template>
<style scoped>
  input {
    width: 17.78vw;
    height: 3.47vw;
    border-radius: 1.735vw;
    margin-top: 1.46vw;
    border: 0.1vw solid #797979;
    -webkit-box-sizing: border-box;
    box-sizing: border-box;
    border-radius: 2vw;
    font-size: 1vw;
    color: rgba(55, 63, 65, 0.61);
    padding: 0vw 1vw;
  }
</style>
