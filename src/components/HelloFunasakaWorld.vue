<script setup>
import {ref} from "vue";

defineProps({
  msg: {
    type: String,
    required: true
  }
})

// リアクティブっぽいこと
const countReactive = ref(0);
const incrementReactive = () => {
    countReactive.value++;
}
const resetReactive = () => {
    countReactive.value = 0;
}

// 普通の変数でやった場合 
const countNormal = 0;
const incrementNormal = () => {
    this.countNormal++;
}
const resetNormal = () => {
    this.countNormal = 0;
}

// テキスト入力
const text = ref("");
</script>

<template>
  <div class="greetings frame-line-yellow">
    <h1 class="green">{{ msg }}</h1>
    <h3>This Area is Funasaka's Area.</h3>
    <br>
    <div class="counter">
        <div>countReactive = {{countReactive}}</div>
        <button @click="incrementReactive">Count up(Reactive)</button>
        <button @click="resetReactive">Reset(Reactive)</button>
    </div>
    <div class="counter">
        <div>countNormal = {{countNormal}}</div>
        <button @click="incrementNormal">Count up(Normal)</button>
        <button @click="resetNormal">Reset(Normal)</button>
    </div>
    <div class="inputText">
        <div>inputText = {{text}}</div>
        <input type="text" v-model="text" placeholder="テキスト入力"/>
    </div>
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
.inputText {
    border: green 1px solid;
    border-radius: 10px;
}
</style>