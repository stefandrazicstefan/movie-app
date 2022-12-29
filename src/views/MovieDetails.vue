<script setup lang="ts">
import { ref, onMounted, nextTick, onBeforeMount } from "vue";
import { useRoute } from "vue-router";
import { IntersectingCirclesSpinner } from "epic-spinners";

const route = useRoute();
const movie = ref<any>({});
const loading = ref(true);

async function fetchData() {
  try {
    const response = await fetch(
      `https://api.themoviedb.org/3/movie/${route.params.slug}?api_key=caba2c307ff756497e9f4b055f16c36b`
    );
    const data = await response.json();
    movie.value = data;
  } catch (error) {
    console.error(error);
  } finally {
    loading.value = false;
  }
}
fetchData();
</script>
<template>
  <intersecting-circles-spinner
    :animation-duration="1200"
    :size="90"
    class="spinner"
    color="green"
    v-if="loading"
  />
  <div
    class="movie-details-wrapper"
    v-else
  >
    <div class="movie-details">
      <section class="left">
        <img
          :src="`http://image.tmdb.org/t/p/w500/${movie.poster_path}`"
          alt=""
        />
      </section>
      <section class="right">
        <h1>{{ movie.title }}</h1>
        <div class="genres">
          <h2 v-for="genre in movie.genres">{{ genre.name }}</h2>
        </div>
        <p v-if="movie.overview">{{ movie.overview }}</p>
        <p v-else>Movie has no overview.</p>
      </section>
    </div>
    <section class="bottom-section">
      <img
        :src="`http://image.tmdb.org/t/p/w500/${movie.backdrop_path}`"
        alt=""
        class="backdrop"
      />
      <p>{{ movie.tagline }}</p>
    </section>
  </div>
</template>

<style></style>
