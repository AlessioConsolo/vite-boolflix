<template>
  <div>
    <AppHeader @search="search" />
    <main>
      <FilmSection :searchQuery="searchQuery" />
    </main>
  </div>
</template>

<script>
import AppHeader from "./components/AppHeader.vue";
import FilmSection from "./components/FilmSection.vue";

export default {
  components: { AppHeader, FilmSection },
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
