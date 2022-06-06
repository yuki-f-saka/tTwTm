<script setup>
defineProps({
  msg: {
    type: String,
    required: true
  }
})
</script>

<template>
  <div class="greetings frame-line-yellow">
    <h1 class="green">{{ msg }}</h1>
    <h3>This Area is Funasaka's Area.</h3>
  </div>
</template>

<style scoped>
.frame-line-yellow {
    border: yellow 1rem dotted;
}
</style>