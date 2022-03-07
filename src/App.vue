<template>
  <div id="app">
    <div class="container">
      <div class="text-center">
        <h2 class="text-center mt-5">Trending Movies 🍿</h2>
        <p>Keep up with the hottest movies that are trending this week.</p>
      </div>

      <div class="my-4">
        <a href="#" @click="getTrendingMovies('day')" class="mx-3 h4">
          Trending today</a
        >
        <a href="#" @click="getTrendingMovies('week')" class="mx-3 h4"
          >This week</a
        >
      </div>

      <div class="row" v-if="movies.length > 0">
        <div class="col-md-3" v-for="(movie, i) in movies" :key="i">
          <movie-card :movie="movie" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from '@vue/reactivity';
import MovieCard from "./components/MovieCard.vue";
import { onMounted } from '@vue/runtime-core';
export default {
  setup() {
    const movies = ref([]);
    const apiKey = ref("9d295bfac80df197274af26d7eb81087");
    
    const getTrendingMovies = async (category) => {
      return fetch(
        `https://api.themoviedb.org/3/trending/movie/${category}?api_key=9d295bfac80df197274af26d7eb81087`
      )
        .then((response) => response.json())
        .then((data) => {
          movies.value = data.results;
        });
    };

    onMounted(async () => {
      await getTrendingMovies("day");
    });

    return {
      movies,
      apiKey,
      getTrendingMovies,
    }
  },
  name: 'App',
  components: {
    MovieCard,
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
