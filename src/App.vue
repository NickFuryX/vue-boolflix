<template>
  <div>
    <searc-bar-component @searchText="searchFunction" />
    <main-component />
    <div>
      <button>prova</button>
      <ul>
        <li v-for="item in findedFilm" :key="item.id">
          {{ item }}
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import MainComponent from "./components/MainComponent.vue";
import SearcBarComponent from "./components/SearcBarComponent.vue";

export default {
  name: "App",
  components: {
    SearcBarComponent,
    MainComponent,
  },
  data() {
    return {
      apiURL: "https://api.themoviedb.org/3/search/",
      apiKey: "84fac8a877bc617c11655d0d1ee8494c",
      findedFilm: [],
    };
  },
  methods: {
    searchFunction() {
      let paramsObj = {
        params: {
          language: "it-IT",
          api_key: this.apiKey,
          query: this.text, //////mettere inputText
        },
      };
      axios.get(this.apiURL + "movie/", paramsObj).then((res) => {
        this.findedFilm = res.data.results;
        console.log(this.findedFilm);
      });
    },
  },
};
</script>

<style lang="scss">
@import "./style/generals.scss";
</style>
