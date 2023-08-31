<template>
    <el-container>
        <el-menu
            default-active="2"
            class="el-menu-vertical-demo"
            :collapse="isCollapse"
        >
        <router-link to="/">
          <el-menu-item index="1">
          <el-icon><icon-menu /></el-icon>
          <template #title>Navigator Two</template>
          </el-menu-item>
        </router-link>
      <router-link to="/about">
        <el-menu-item index="3">
          <el-icon><setting /></el-icon>
          <template #title>Navigator Four</template>
        </el-menu-item> 
      </router-link>
  </el-menu>
    </el-container>
</template>

<style scoped>
.collapse-enter-active,
.collapse-leave-active {
    transition: all 0.2s;
}
.collapse-enter,
.collapse-leave-to {
    opacity: 0;
    transform: translateX(-100%);
}

.el-menu-vertical-demo:not(.el-menu--collapse) {
  width: 200px;
  min-height: 400px;
}
</style>

<script setup>
import { ref } from 'vue'
import { RouterLink } from 'vue-router'

import {
  Document,
  Menu as IconMenu,
  Location,
  Setting,
} from '@element-plus/icons-vue'

const isCollapse = ref(true)
</script>
