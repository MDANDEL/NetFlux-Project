<template>
  <h2 id="popular-title">Popular</h2>
  <div id="popular">
    <div class="row">
      <Image
        v-for="movie in popular_movies"
        v-bind:key="movie"
        :img="movie.img"
        :name="movie.name"
        v-on:click="getPopularMovies()"
      />
    </div>
  </div>
</template>

<script>

import Image from "./components/ImageMovie.vue"

export default {
  name: "App",
  components: {
    Image
  },
  methods: {
    async getPopularMovies() {
      let response = await fetch(
        `https://api.themoviedb.org/3/movie/popular?api_key=a7ac5b024a2bd5fe31e06534b18a0b26`
      );
      let data = response.json();
      for (let i = 0; i < data.length; i++) {
        this.popular_movies.push({
          img: `https://image.tmdb.org/t/p/original${data[i].poster_path}`,
          name: data[i].title,
          id: data[i].id,
        });
      }
    },

    async created() {
      await this.getPopularMovies();
    },
  },
};
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