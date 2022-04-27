<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <div style="margin: 20px; display: flex; justify-content: center; align-items: center;">
    <a-button style="margin-right: 10px"><RouterLink to="/">Home</RouterLink></a-button>
    <a-button><RouterLink to="/about">About</RouterLink></a-button>
  </div>
  <router-view v-slot="{ Component }">
    <keep-alive>
      <component :is="Component" />
    </keep-alive>
  </router-view>
</template>

