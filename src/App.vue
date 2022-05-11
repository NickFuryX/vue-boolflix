<template>
  <div id="app">
    <header>
      <h1 class="display-6">Boolflix</h1>
      <search-bar @performSearch="search" />
    </header>
    <main>
      <grid-list :items="movies" title="Movies" :loader="loading" />
      <grid-list :items="series" title="Series" :loader="loadingSeries" />
    </main>
  </div>
</template>

<script>
import GridList from './components/GridList.vue'
import SearchBar from './components/SearchBar.vue'
import axios from 'axios'

export default {
  name: 'App',
  components: {
    SearchBar,
    GridList
  },
  data(){
    return{
      apiKey: 'e99307154c6dfb0b4750f6603256716d',
      apiPath: 'https://api.themoviedb.org/3/search/',
      movies:[],
      series:[],
      loading: false,
      loadingSeries: false
    }
  },
  methods:{
    chageUk(){
      if(this.movies.original_language === 'en'){
        this.movies.original_language == 'gb'
        console.log('lingua letta');
      } else{
        console.log('non ha funzionato');
      }
    },
    getMovies(queryParams){
      axios.get(this.apiPath+'movie', queryParams).then((res)=>{
        //console.log(res.data.results)
        this.movies = res.data.results;
        this.loading = false;
      }).catch((error)=>{
        console.log(error);
      });
      this.chageUk(this.movies)

    },
     search(text){
       const queryParams = {
        params:{
          api_key: this.apiKey,
          language: 'it-IT',
          query: text
        }
      }
      this.loading = true;
      this.loadingSeries = true;
      this.getMovies(queryParams);
      this.getSeries(queryParams);
    },
    getSeries(queryParams){
      axios.get(this.apiPath+'tv', queryParams).then((res)=>{
        //console.log(res.data.results)
        this.series = res.data.results;
        this.loadingSeries = false;
      }).catch((error)=>{
        console.log(error);
      })
    },

  }
 }
</script>

<style lang="scss">
@import "./styles/general.scss";
</style>
