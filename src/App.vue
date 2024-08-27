<template>
  <div>
    <AppHeader @search="search" />
    <main>
      <FilmSection :searchQuery="searchQuery" />
      <TVSection :searchQuery="searchQuery" />
    </main>
  </div>
</template>

<script>
import AppHeader from "./components/AppHeader.vue";
import FilmSection from "./components/FilmSection.vue";
import TVSection from "./components/TVSection.vue";

export default {
  components: { AppHeader, FilmSection, TVSection },
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
