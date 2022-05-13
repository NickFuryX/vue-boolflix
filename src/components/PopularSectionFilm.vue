<template>
  <div >
    <h2 class="ps-4">Film popolari su Boolflix</h2>
    <div class="popular-div"> 
        <card-boolflix v-for="item in items" :key="item.id" :cardItem="item" />
    </div>
  </div>
</template>

<script>
import CardBoolflix from "./CardBoolflix.vue";
export default {
  components: { CardBoolflix },
  name: "PopularSectionFilm",
  props: {
    items: Array,
  },
  data() {
    return {};
  },
};
</script>

<style scoped lang="scss">
h2 {
  color: white;
  font-size: 40px;
}
.popular-div {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
  justify-content: center;
}
</style>
