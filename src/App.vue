<script setup>
import { RouterView } from 'vue-router'
import NavBar from './components/NavBar.vue'
import SideBar from './components/SideBar.vue'
</script>

<template>
  <div class="p-4 sm:ml-64">
    <div class="p-4  mt-14">
      <NavBar />
      <SideBar />
      <RouterView />
    </div>
  </div>
</template>
