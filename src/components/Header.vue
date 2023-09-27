<template>
<div class="header">
  <a  v-for="n in navList" :class="$route.path==n.link?'is-active':''" :href='n.link'>{{n.title}}</a>
</div>
</template>

<style>
.header{
  display: flex;
  justify-content: flex-start;
  align-items: center;
  gap: 30px;
  background-color: #f4f4f4;
  height: 4rem;
}
.header a{
  text-decoration: none;
  color: #797979;
  display: inline-flex;
  height: 2.5rem;
  padding: 0 1rem;
  align-items: center;
  justify-content: center;

  border-radius: 25px;
}
.header .is-active{
  color: #222323;
  background-color: #edeef0;
}
.header .is-active, .header a:hover{
  background-color: #edeef0;
}
</style>
<script setup lang="ts">
const navList = [
  {
    link:"/",title:"第一题"
  },
  {
    link:"/second",title:"第二题"
  },
  {
    link:"/third",title:"第三题"
  }
]
</script>



