<template>
  <section>
    <h2 class="text-white">{{ title }}</h2>
    <div class="main-container">
      <CardBoolflix v-for="item in items" :key="item.id" :cardItem="item" />
      <!-- <div>
        <ul>
          <li v-for="item in items" :key="item.id">
            id: {{ item.id }}<br />
            titolo originale:
            {{ item.original_title ? item.original_title : item.original_name
            }}<br />
            titolo: {{ item.title ? item.title : item.name }}<br />
            lingua originale:
            <country-flag
              v-if="
                item.original_language === 'en'
                  ? (item.original_language = 'gb')
                  : (item.original_language = item.original_language)
              "
              :country="item.original_language"
              size="small"
            /><br />
            voto: {{ item.vote_average }}<br />
            <img :src="apiImgPath + item.poster_path" alt="" />
          </li>
        </ul>
      </div> -->
    </div>
  </section>
</template>

<script>
import CardBoolflix from "./CardBoolflix.vue";
//import {state, actions} from '../store.js'
export default {
  name: "GridList",
  components: {
    CardBoolflix,
  },
  props: {
    items: Array,
    loader: Boolean,
    title: String,
  }, //['items','loader'],
  data() {
    return {
      apiImgPath: "https://image.tmdb.org/t/p/w342",
    };
  },
  computed: {
  
  },
  methods: {},
};
</script>

<style lang="scss">
.main-container{
  display: flex;
  flex-wrap: wrap;
}
</style>
