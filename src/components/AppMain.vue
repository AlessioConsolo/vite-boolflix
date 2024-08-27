<template>
  <div>
    <input type="text" v-model="searchQuery" />
    <button @click="searchMovies">Cerca</button>
    <ul>
      <li v-for="movie in movies" :key="movie.id">
        {{ movie.title }} <br />
        {{ movie.original_title }} <br />
        {{ movie.original_language }} <br />
        {{ movie.vote_average }}
      </li>
    </ul>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      searchQuery: "",
      movies: [],
    };
  },
  methods: {
    searchMovies() {
      axios
        .get(
          `https://api.themoviedb.org/3/search/movie?api_key=cb4e8200a9d894d0b396d2d7fe14c7ed&query=${this.searchQuery}`
        )
        .then((response) => {
          this.movies = response.data.results;
        })
        .catch((error) => {
          console.error(error);
        });
    },
  },
};
</script>
