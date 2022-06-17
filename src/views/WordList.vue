<script setup>
  import { ref } from "vue";
  const itWord = ref("WordA");


</script>

<template>
  <v-card style="margin-top:10px">
    <v-card-title primary-title> <!-- 説明 3.11 -->
      <h1 class="headline">Title:wordList</h1>
    </v-card-title>

    <div style="margin: 10px 20px;">
      <div class="scroll-erea">

      </div>
      <textarea style='width:100%; height:300px; background-color:#efefef; padding:3px'>
        <v-btn>  
          {{itWord}} 
        </v-btn>
      </textarea>
    </div>
  </v-card>


</template>

<!-- <style>
@media (min-width: 1024px) {
  .WordListTitle {
    min-height: 100vh;
    display: flex;
    align-items: center;
  }
}
@media (min-width: 1024px) {
  .Word {
    min-height: 150vh;
    display: block;
    align-items: center;
  }
}
</style> -->
