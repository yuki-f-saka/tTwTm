<template>
<!-- 下のclass="kSample"はスタイルタグ内で設定したもの -->
  <div class="kSample">
    <h1>This page is sample for me</h1>
  </div>
  <div class="kSample">
    <h2>This is h2</h2>
    <p>This is P tag</p>
  </div>
</template>

<style>
@media (min-width: 1024px) {
  .kSample {
    min-height: 100vh;
    display: flex;
    align-items: center;
  }
}
</style>
