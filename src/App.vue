<template>
  <div id="app">
    <header>
      <app-search @performSearch="search" />
    </header>
    <main>
      <app-grid :items="movies" title="Movies" :loader="loading" />
      <app-loader v-if="loadingSeries" />
      <app-grid :items="series" title="Series" :loader="loadingSeries" />
    </main>
  </div>
</template>

<script>
import axios from "axios";
import AppSearch from "./components/AppSearch.vue";
import AppGrid from "./components/AppGrid.vue";

export default {
  name: "App",
  components: {
    AppSearch,
    AppGrid,
  },
  data() {
    return {
      apiKey: "2589d2905f389ff857757725b41a87bf",
      apiURL: "https://api.themoviedb.org/3/search/",
      movies: [],
      series: [],
      loading: false,
      loadingSeries: false,
    };
  },
  methods: {
    getMovies(queryParams) {
      axios
        .get(this.apiURL + "movie", queryParams)
        .then((res) => {
          this.movies = res.data.results;
          this.loading = false;
        })
        .catch((error) => {
          console.log(error);
        });
    },
    getSeries(queryParams) {
      axios
        .get(this.apiURL + "tv", queryParams)
        .then((res) => {
          this.series = res.data.results;
          this.loadingSeries = false;
        })
        .catch((error) => {
          console.log(error);
        });
    },
    search(text) {
      const queryParams = {
        params: {
          api_key: this.apiKey,
          query: text,
        },
      };
      this.loading = true;
      this.loadingSeries = true;
      this.getMovies(queryParams);
      this.getSeries(queryParams);
    },
  },
};
</script>

<style lang="scss">
@import "./style/general.scss";
@import "./style/vars.scss";
header {
  height: 60px;
  background-color: $bg-header;
  h1 {
    color: $color-title;
  }
}
main {
  background-color: $bg-main;
  h2 {
    padding-left: 48px;
    color: $color-info;
    font-weight: 900;
  }
}
</style>
