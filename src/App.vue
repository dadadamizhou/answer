<script setup lang="ts">

import Header from "./components/Header.vue";
</script>

<template>
  <div class="custom-container">
    <div>
      <Header/>
    </div>
    <div class="main">
      <router-view/>
    </div>
  </div>
</template>

<style>
div{
  display: block;
}
body {
  margin: 0px;
  font-size: 16px;
}
.custom-container{
  display: grid;
  grid-template-rows: auto 1fr auto;
  min-height: 100vh;
}
.main{
  display: flex;
  justify-content: center;
  align-items: center;
  color: #f3dfe5;
  background-color: #ece8ea;
}
</style>
