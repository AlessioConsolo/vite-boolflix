<template>
  <section>
    <h2>Serie TV</h2>
    <ul>
      <li v-for="tvShow in tvShows" :key="tvShow.id">
        <div
          class="card"
          @mouseover="hoveredTvShowId = tvShow.id"
          @mouseleave="hoveredTvShowId = null"
        >
          <img
            :src="`https://image.tmdb.org/t/p/w342${tvShow.poster_path}`"
            alt="Copertina della serie TV"
            class="card-img-top"
            :style="{ opacity: hoveredTvShowId === tvShow.id ? 0 : 1 }"
          />
          <div class="card-overlay" v-if="hoveredTvShowId === tvShow.id">
            <div class="card-info">
              {{ tvShow.name }} <br />
              {{ tvShow.original_name }} <br />
              <span v-html="getFlagIcon(tvShow.original_language)"></span>
              <br />
              <div class="rating">
                <i
                  v-for="n in getRating(tvShow.vote_average)"
                  :key="n"
                  class="fa-solid fa-star"
                ></i>
                <i
                  v-for="n in 5 - getRating(tvShow.vote_average)"
                  :key="n"
                  class="fa-regular fa-star"
                ></i>
              </div>
              <br />
              {{ tvShow.overview }}
            </div>
          </div>
        </div>
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
      hoveredTvShowId: null,
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

<style>
.card {
  position: relative;
  width: 342px;
  height: 300px;
  border: 1px solid #ddd;
  border-radius: 10px;
  overflow: hidden;
}

.card-img-top {
  width: 342px;
  height: 500px;
  object-fit: cover;
  transition: opacity 0.3s ease-in-out;
}

.card-overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.8);
  display: flex;
  justify-content: center;
  align-items: center;
}

.card-info {
  color: #fff;
  font-size: 16px;
  padding: 20px;
  text-align: center;
  overflow-y: auto;
}

.rating {
  display: inline-block;
}

ul {
  list-style-type: none;
  padding: 0;
  margin: 0;
  display: flex;
  flex-wrap: wrap;
}

li {
  display: inline-block;
  margin: 10px;
}
</style>
