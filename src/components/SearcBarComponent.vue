<template>
  <div class="input-group ms-5 mt-5">
    <div class="form-outline">
      <input
        type="search"
        class="form-control"
        placeholder="Search"
        v-model="inputText"
      />
    </div>
    <button @click="$emit('searchText', inputText)" type="button" class="btn btn-primary">
      <i class="fas fa-search"></i>
    </button>
  </div>
</template>

<script>
export default {
  name: "SearcBarComponent",
  data(){
    return{
      inputText: ''
    }
  }
  
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss">
@import "../style/generals.scss";
</style>
