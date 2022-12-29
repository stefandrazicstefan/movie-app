<script setup lang="ts">
import { ref } from "vue";

const props = defineProps({
  title: String,
  imgPath: String,
  id: Number,
});
</script>

<template>
  <router-link
    :to="`/${props.id}`"
    class="router"
  >
    <div class="single-movie">
      <h2>{{ title }}</h2>
      <img
        :src="imgPath"
        alt=""
      />
    </div>
  </router-link>
</template>

<style scoped>
div {
  color: green;
}
</style>
