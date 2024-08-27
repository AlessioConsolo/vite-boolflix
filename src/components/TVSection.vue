<template>
  <section>
    <h2>Serie TV</h2>
    <ul>
      <li v-for="tvShow in tvShows" :key="tvShow.id">
        {{ tvShow.name }} <br />
        {{ tvShow.original_name }} <br />
        {{ tvShow.original_language }} <br />
        {{ tvShow.vote_average }}
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
      tvShows: [],
    };
  },
  watch: {
    searchQuery(newSearchQuery) {
      this.searchTVShows(newSearchQuery);
    },
  },
  methods: {
    searchTVShows(searchQuery) {
      axios
        .get(
          `https://api.themoviedb.org/3/search/tv?api_key=cb4e8200a9d894d0b396d2d7fe14c7ed&query=${searchQuery}`
        )
        .then((response) => {
          this.tvShows = response.data.results;
        })
        .catch((error) => {
          console.error(error);
        });
    },
  },
};
</script>
