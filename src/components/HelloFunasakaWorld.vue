<script setup>
import {ref} from "vue";

defineProps({
  msg: {
    type: String,
    required: true
  }
})

const count = ref(0);
const increment = () => {
    count.value++;
}
const reset = () => {
    count.value = 0;
}
</script>

<template>
  <div class="greetings frame-line-yellow">
    <h1 class="green">{{ msg }}</h1>
    <h3>This Area is Funasaka's Area.</h3>
    <br>
    <div class="counter">count = {{count}}</div>
    <button @click="increment">Count up</button>
    <button @click="reset">Reset</button>
  </div>
</template>

<style scoped>
.frame-line-yellow {
    border: yellow 1rem dotted;
}
.counter {
    border: red 1px solid;
    border-radius: 10px;
}
</style>