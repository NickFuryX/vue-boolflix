<template>
  <section>
    <h2 class="text-white">{{ title }}</h2>
    <div class="main-container">
      <CardBoolflix v-for="item in items" :key="item.id" :cardItem="item" />
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
  gap: 20px;
  justify-content: center;
}
</style>
