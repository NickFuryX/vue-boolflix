<template>
  <div class="my-card">
    <!-- id: {{ localItem.id }}<br /> -->
    <img :src="apiImgPath + localItem.poster_path" alt="" />
    <div class="info-card">
        <div>
            Titolo originale:
            {{
              localItem.original_title
                ? localItem.original_title
                : localItem.original_name
            }}
        </div>
        <div>Titolo: {{ localItem.title ? localItem.title : localItem.name }}</div>
        <div>
          <div v-if="flag.includes(localItem.original_language)">
              lingua originale:
              <lang-flag :iso="localItem.original_language" :squared="false" />
          </div>
          <div v-else>
          Lingua originale: {{localItem.original_language}}

          </div>
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
      apiImgPath: "https://image.tmdb.org/t/p/w342",
      localItem: this.cardItem,
      flag: relation
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
  background-color: rgb(100, 125, 140);
  display: flex;
  flex-direction: column;
  padding-top: 5px;
  border-radius: 5px;
  

  img {
    width: 95%;
    height: 60%;
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
.info-card{
    widows: 95%;
    padding: 5px;
}
</style>
