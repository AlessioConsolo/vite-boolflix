<template>
  <div class="container-fluid bg-dark py-5 mb-4">
    <div class="row">
      <div class="col">
        <h1 class="text-danger text-center pb-3">BoolFlix</h1>
        <header class="text-center">
          <input type="text" v-model="searchQuery" />
          <button class="ms-2" @click="$emit('search', searchQuery)">
            Cerca
          </button>
        </header>
      </div>
    </div>
  </div>
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

<style lang="scss"></style>
