<template>
  <div class="my-card">
      <ul >
        <li>
          <!-- id: {{ localItem.id }}<br /> -->
          <img :src="apiImgPath + localItem.poster_path" alt="" /><br />
          titolo originale:
          {{
            localItem.original_title
              ? localItem.original_title
              : localItem.original_name
          }}<br />
          titolo: {{ localItem.title ? localItem.title : localItem.name }}<br />
          lingua originale:
          <country-flag
            v-if="
              localItem.original_language === 'en'
                ? (localItem.original_language = 'gb')
                : (localItem.original_language = localItem.original_language)
            "
            :country="localItem.original_language"
            size="small"
          /><br />
          <!-- <div class="starAdd">voto: {{ starFunction }}</div> <br /> -->
          <div id="starAdd">voto: <i class="fa-solid fa-star"></i></div>
        </li>
      </ul>
  </div>
</template>

<script>
import CountryFlag from "vue-country-flag";
export default {
  name: "CardBoolflix",
  components: {
    CountryFlag,
  },
  props: ["cardItem"], //['items','loader'],
  data() {
    return {
      apiImgPath: "https://image.tmdb.org/t/p/w185",
      localItem: this.cardItem,
    };
  },
  computed: {
    // starFunction() {
    //   let votoSuCinque = Math.ceil(this.localItem.vote_average / 2);
    //   let pointAdd = document.getElementById("starAdd");
    //   for (let i = 0; i < votoSuCinque; i++) {
    //     let star = document.createElement("i");
    //     star.classList.add("fa-solid");
    //     star.classList.add("fa-star");
    //     pointAdd.append(star)
    //   }
    //   return this.pointAdd;
    // },
  },
  methods: {},
};
</script>

<style lang="scss">
.my-card{
    width: calc(100% / 6);
    height: 450px;
    img{
        width: 100%;
    }
}
ul {
  color: white;
}
li {
  list-style-type: none;
}
</style>
