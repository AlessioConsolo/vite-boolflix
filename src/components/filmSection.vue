<template>
  <section>
    <h2>Film</h2>
    <ul>
      <li v-for="movie in movies" :key="movie.id">
        {{ movie.title }} <br />
        {{ movie.original_title }} <br />
        <span v-html="getFlagIcon(movie.original_language)"></span> <br />
        {{ movie.vote_average }}
      </li>
    </ul>
  </section>
</template>

<script>
import axios from "axios";

export default {
  props: ["searchQuery"],
  data() {
    return {
      movies: [],
    };
  },
  watch: {
    searchQuery(newSearchQuery) {
      this.searchMovies(newSearchQuery);
    },
  },
  methods: {
    searchMovies(searchQuery) {
      axios
        .get(
          `https://api.themoviedb.org/3/search/movie?api_key=cb4e8200a9d894d0b396d2d7fe14c7ed&query=${searchQuery}`
        )
        .then((response) => {
          this.movies = response.data.results;
        })
        .catch((error) => {
          console.error(error);
        });
    },
    getFlagIcon(nationalityCode) {
      const validCodes = ["en", "fr", "es", "it", "de", "pt", "zh", "ja", "ko"];

      if (validCodes.includes(nationalityCode.toLowerCase())) {
        return `<span class="fi fi-${nationalityCode.toLowerCase()}"></span>`;
      } else {
        return "";
      }
    },
  },
};
</script>
