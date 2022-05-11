<template>
  <section>
    <h2>{{ title }}</h2>
    <ul>
      <li v-for="item in items" :key="item.id">
        id: {{ item.id }}<br />
        titolo originale: {{ item.original_title }}<br />
        titolo: {{ item.title }}<br />
        <!-- lingua originale: {{ item.original_language }}<br /> -->
        lingua originale: <country-flag :country='item.original_language' size='small'/><br />
        

        voto: {{ item.vote_average }}<br />
      </li>
    </ul>
  </section>
</template>

<script>
import CountryFlag from "vue-country-flag";
//import {state, actions} from '../store.js'
export default {
  name: "GridList",
  components: {
    CountryFlag,
  },
  props: {
    items: Array,
    loader: Boolean,
    title: String,
  }, //['items','loader'],
  data() {
    return {};
  },
  computed: {
    // mysearch(){
    //     return state.search
    // }
  },
  methods: {
    // leggi(){
    //     actions.setSearch('aaaaa')
    // }
  },
};
</script>

<style lang="scss"></style>
