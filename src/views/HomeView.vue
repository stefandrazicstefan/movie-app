<script setup lang="ts">
import { ref, onMounted, nextTick } from "vue";
import Movie from "../components/Movie.vue";
import { IntersectingCirclesSpinner } from "epic-spinners";

const query = ref("");
const movies = ref<any>({});
const loading = ref(false);

async function fillObject() {
  loading.value = true;
  try {
    const response = await fetch(
      `https://api.themoviedb.org/3/search/movie?api_key=caba2c307ff756497e9f4b055f16c36b&query=${query.value}`
    );
    const data = await response.json();
    movies.value = data.results;
    if (movies.value.length < 1) alert("No movies found");
  } catch (error) {
    console.error(error);
  } finally {
    loading.value = false;
  }
}
</script>

<template>
  <main>
    <form
      action=""
      @submit.prevent="fillObject"
    >
      <input
        type="text"
        v-model="query"
        placeholder="movie name"
      />
    </form>
    <intersecting-circles-spinner
      :animation-duration="1200"
      :size="90"
      class="spinner"
      color="green"
      v-if="loading"
    />
    <div
      class="movies"
      v-else
    >
      <Movie
        v-for="movie in movies"
        :title="movie.title"
        :id="movie.id"
        :img-path="`http://image.tmdb.org/t/p/w500/${movie.poster_path}`"
        :key="movie.id"
      />
    </div>
  </main>
</template>
