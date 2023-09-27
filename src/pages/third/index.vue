<template>
  <div class="container">
    <Avatar
        class="item"
        :size="80"
        v-for="(avatar,index ) in avatars"
        :key="index"
        :style="{ top: avatar.top + 'px' ,left: avatar.left + 'px' }"
    />
  </div>
</template>

<script setup lang="ts">
import Avatar from "vue-boring-avatars";
import { onMounted, ref, computed } from "vue";

const scrollY = ref(0);
const handleScroll = () => {
  scrollY.value = window.scrollY;
};

onMounted(() => {
  window.addEventListener('scroll', handleScroll);
});

const initPosition = [
  {
    "top": 500,
    "left": 80,
    "scrollFactor": 0.7,
  },
  {
    "top": 500,
    "left": 130,
    "scrollFactor": 0.6,
  },
  {
    "top": 460,
    "left": 280,
    "scrollFactor": 0.6,
  },
  {
    "top": 460,
    "left": 320,
    "scrollFactor": 0.8,
  },
  {
    "top": 490,
    "left": 430,
    "scrollFactor": 0.6,
  },
  {
    "top": 430,
    "left": 480,
    "scrollFactor": 1,
  },
  {
    "top": 460,
    "left": 580,
    "scrollFactor": 0.7,
  },
  {
    "top": 490,
    "left": 660,
    "scrollFactor": 0.8,
  },
]

const avatars = computed(() => {

  return initPosition.map((position) => {
    return {
      top: position.top - scrollY.value * position.scrollFactor ,
      left: position.left
    };
  });
});
</script>

<style>
.container {
  height: 1200px;
}
.item {
  position: fixed;
}
</style>
