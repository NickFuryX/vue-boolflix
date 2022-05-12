<template>
  <div class="my-card">
    <!-- id: {{ localItem.id }}<br /> -->
    <img :src="imgFunction" alt="" />
    <div class="info-card">
      <div>
        Titolo originale:
        {{
          localItem.original_title
            ? localItem.original_title
            : localItem.original_name
        }}
      </div>
      <div>
        Titolo: {{ localItem.title ? localItem.title : localItem.name }}
      </div>
      <div>
        <div v-if="flag.includes(localItem.original_language)">
          lingua originale:
          <lang-flag :iso="localItem.original_language" :squared="false" />
        </div>
        <div v-else>Lingua originale: {{ localItem.original_language }}</div>
      </div>
      <div class="starAdd">
        Voto:
        <span v-for="(n, index) in 5" :key="index">
          <i
            :class="
              n <= starFunction
                ? 'fa-solid fa-star golden-star'
                : 'fa-solid fa-star'
            "
          ></i>
        </span>
      </div>
      <div class="overview">Overview: {{ localItem.overview }}</div>
    </div>
  </div>
</template>

<script>
// import CountryFlag from "vue-country-flag";
import LangFlag from "vue-lang-code-flags";
import relation from "../bandiere";

export default {
  name: "CardBoolflix",
  components: {
    // CountryFlag,
    LangFlag,
  },
  props: ["cardItem"], //['items','loader'],
  data() {
    return {
      apiImgPath: "https://image.tmdb.org/t/p/w500",
      localItem: this.cardItem,
      flag: relation,
    };
  },
  computed: {
    starFunction() {
      let votoSuCinque = Math.ceil(this.localItem.vote_average / 2);
      return votoSuCinque;
    },
    imgFunction() {
      if (this.cardItem.poster_path === null) {
        return require('../assets/img/fotoNotFound.jpg')
      } else {
        return this.apiImgPath + this.localItem.poster_path;
      }
    },
  },
  methods: {},
};
</script>

<style lang="scss">
.my-card {
  cursor: pointer;
  width: calc((100% - 120px) / 5);
  height: 450px;
  background-color: rgb(100, 125, 140);
  display: flex;
  flex-direction: column;
  padding-top: 5px;
  padding-bottom: 5px;

  &:hover img {
    display: none;
  }
  &:hover .info-card {
    display: block;
    overflow-y: hidden;
  }

  border-radius: 5px;
  position: relative;

  img {
    width: 95%;
    height: 100%;
    margin: 0 auto;
  }
}
ul {
  color: white;
}
li {
  width: 100%;
  list-style-type: none;
}
.golden-star {
  color: #ffd700;
}
.info-card {
  widows: 95%;
  padding: 5px;
  position: absolute;
  display: none;
}

</style>
