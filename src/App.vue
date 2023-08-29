<script setup>
import { RouterLink, RouterView } from 'vue-router'
import SideNav from '@/components/SideNav.vue'
</script>

<template>
  <div>
    <div class="nav-container">
      <SideNav></SideNav>
    </div>
    <div class="content">
      <RouterView />
    </div>
  </div>
</template>

<style scoped>
.nav-container{
  position:fixed;
  z-index: 3;
}
.content{
  margin-left: 10%;
}
</style>
