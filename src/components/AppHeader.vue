<template>
  <header>
    <input type="text" v-model="searchQuery" />
    <button @click="$emit('search', searchQuery)">Cerca</button>
  </header>
</template>

<script>
export default {
  data() {
    return {
      searchQuery: "",
    };
  },
};
</script>
