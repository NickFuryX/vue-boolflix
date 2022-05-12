<template>
  <div class="my-card">
    <!-- id: {{ localItem.id }}<br /> -->
    <img :src="apiImgPath + localItem.poster_path" alt="" />
    titolo originale:
    {{
      localItem.original_title
        ? localItem.original_title
        : localItem.original_name
    }}
    titolo: {{ localItem.title ? localItem.title : localItem.name }} lingua
    originale: <lang-flag :iso="localItem.original_language" :squared="false" />

    <div class="starAdd">
      voto:
      <span v-for=" (n, index) in 5" :key=" index">
      <i :class="n <= starFunction ? 'fa-solid fa-star golden-star' : 'fa-solid fa-star' "></i>
      </span>
    </div>
  </div>
</template>

<script>
// import CountryFlag from "vue-country-flag";
import LangFlag from "vue-lang-code-flags";

export default {
  name: "CardBoolflix",
  components: {
    // CountryFlag,
    LangFlag,
  },
  props: ["cardItem"], //['items','loader'],
  data() {
    return {
      apiImgPath: "https://image.tmdb.org/t/p/w342",
      localItem: this.cardItem,
    };
  },
  computed: {
    starFunction() {
      let votoSuCinque = Math.ceil(this.localItem.vote_average / 2);
      return votoSuCinque;
    },
  },
  methods: {},
};
</script>

<style lang="scss">
.my-card {
  width: calc((100% - 120px) / 6);
  height: 450px;
  background-color: aquamarine;
  display: flex;
  flex-direction: column;

  img {
    width: 100%;
    height: 60%;
  }
}
ul {
  color: white;
}
li {
  width: 100%;
  list-style-type: none;
}
.golden-star{
    color: #FFD700;
}
</style>
