<template>
  <body>
    <div class="nav-container">
      <SideNav></SideNav>
    </div>
    <div class="content">
      <RouterView />
    </div>
  </body>
</template>

<style scoped>
body{
  display: flex;
}
.nav-container{
  position:fixed;
  z-index: 3;
  padding-top: 1px;
}
.content{
  margin-left: 10%;
  width: 90%;
}
</style>

<script setup>
import { RouterLink, RouterView } from 'vue-router'
import SideNav from '@/components/SideNav.vue'
</script>

