<template>
  <div id="app">
    <header>
      <h1 class="display-6 css-3d-text text-center">BOOLFLIX</h1>
    </header>
    <main>
      <semipolar-spinner
        v-if="loading"
        :animation-duration="2000"
        :size="500"
        color="#ff1d5e"
      />
      <popular-section-film :items="popularFilms" />
      <popular-section-series :items="popularSeries" />
      <search-bar @performSearch="search" />
      <grid-list :items="movies" title="Movies" :loader="loading" />
      <grid-list :items="series" title="Series" :loader="loadingSeries" />
    </main>
  </div>
</template>

<script>
import GridList from "./components/GridList.vue";
import SearchBar from "./components/SearchBar.vue";
import { SemipolarSpinner } from "epic-spinners";

import axios from "axios";
import PopularSectionFilm from "./components/PopularSectionFilm.vue";
import PopularSectionSeries from "./components/PopularSectionSeries.vue";

export default {
  name: "App",
  components: {
    SearchBar,
    GridList,
    SemipolarSpinner,
    PopularSectionFilm,
    PopularSectionSeries,
  },
  data() {
    return {
      apiKey: "e99307154c6dfb0b4750f6603256716d",
      apiPath: "https://api.themoviedb.org/3/search/",
      popularFilmApiPath:
        "https://api.themoviedb.org/3/movie/popular/?&api_key=84fac8a877bc617c11655d0d1ee8494c&language=it-IT",
      popularSeriesApiPath:
        "https://api.themoviedb.org/3/movie/popular/?&api_key=84fac8a877bc617c11655d0d1ee8494c&language=it-IT",
      movies: [],
      series: [],
      popularFilms: [],
      popularSeries: [],
      loading: false,
      loadingSeries: false,
    };
  },
  mounted() {
    this.getPopularMovies();
    this.getPopularSeries();
  },
  methods: {
    getMovies(queryParams) {
      axios
        .get(this.apiPath + "movie", queryParams)
        .then((res) => {
          //console.log(res.data.results)
          this.movies = res.data.results;
          this.loading = false;
        })
        .catch((error) => {
          console.log(error);
        });
    },
    getPopularMovies() {
      axios.get(this.popularFilmApiPath).then((res) => {
        this.popularFilms = res.data.results;
      });
    },
    getPopularSeries() {
      axios.get(this.popularSeriesApiPath).then((res) => {
        this.popularSeries = res.data.results;
      });
    },
    search(text) {
      const queryParams = {
        params: {
          api_key: this.apiKey,
          language: "it-IT",
          query: text,
        },
      };
      this.loading = true;
      this.loadingSeries = true;
      this.getMovies(queryParams);
      this.getSeries(queryParams);
    },
    getSeries(queryParams) {
      axios
        .get(this.apiPath + "tv", queryParams)
        .then((res) => {
          //console.log(res.data.results)
          this.series = res.data.results;
          this.loadingSeries = false;
        })
        .catch((error) => {
          console.log(error);
        });
    },
  },
};
</script>

<style lang="scss">
@import "./styles/general.scss";
.css-3d-text {
  font-size: 92px;
  color: #d12323;
  font-family: Lucida Console;
  text-shadow: 0px 0px 0 rgb(200, 26, 26), 1px 1px 0 rgb(190, 16, 16),
    2px 2px 0 rgb(181, 7, 7), 3px 3px 0 rgb(172, -2, 0),
    4px 4px 0 rgb(162, -12, 0), 5px 5px 0 rgb(153, -21, 0),
    6px 6px 0 rgb(144, -30, 0), 7px 7px 0 rgb(134, -40, 0),
    8px 8px 0 rgb(125, -49, 0), 9px 9px 0 rgb(116, -58, 0),
    10px 10px 9px rgba(0, 0, 0, 0.6), 10px 10px 1px rgba(0, 0, 0, 0.5),
    0px 0px 9px rgba(0, 0, 0, 0.2);
}
</style>
