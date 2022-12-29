<script setup lang="ts">
import { RouterLink, RouterView } from "vue-router";
</script>

<template>
  <header>
    <router-link
      to="/"
      class="router"
      >Movie app</router-link
    >
  </header>
  <RouterView />
</template>

<style scoped></style>
