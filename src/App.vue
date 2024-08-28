<template>
  <div>
    <AppHeader @search="search" />
    <main>
      <MovieSection :searchQuery="searchQuery" />
      <TVSection :searchQuery="searchQuery" />
    </main>
  </div>
</template>

<script>
import AppHeader from "./components/AppHeader.vue";
import MovieSection from "./components/MovieSection.vue";
import TVSection from "./components/TVSection.vue";

export default {
  components: { AppHeader, MovieSection, TVSection },
  data() {
    return {
      searchQuery: "",
    };
  },
  methods: {
    search(searchQuery) {
      this.searchQuery = searchQuery;
    },
  },
};
</script>
