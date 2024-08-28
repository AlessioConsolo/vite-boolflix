<template>
  <section>
    <h2>Film</h2>
    <ul>
      <li v-for="movie in movies" :key="movie.id">
        {{ movie.title }} <br />
        {{ movie.original_title }} <br />
        <span v-html="getFlagIcon(movie.original_language)"></span> <br />
        <div class="rating">
          <i
            v-for="n in getRating(movie.vote_average)"
            :key="n"
            class="fa-solid fa-star"
          ></i>
          <i
            v-for="n in 5 - getRating(movie.vote_average)"
            :key="n"
            class="fa-regular fa-star"
          ></i>
        </div>
        <br />
        <img
          :src="`https://image.tmdb.org/t/p/w500${movie.backdrop_path}`"
          alt="Copertina del film"
        />
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
    getRating(vote) {
      return Math.ceil(vote / 2);
    },
  },
};
</script>
