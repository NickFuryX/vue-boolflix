<template>
  <div>
    <input
      class="css-input"
      type="text"
      v-model="search"
      @keyup.enter="cerca"
    />
    <button class="myButton" @click="cerca">Cerca</button>
    <select name="" id="" v-model="searchType">
      <option value="movie">Film</option>
      <option value="tv">Serie tv</option>
    </select>
  </div>
</template>

<script>
//import state from '../store.js'
export default {
  name: "SearchBar",
  data() {
    return {
      search: "",
      searchType: "",
    };
  },
  computed: {
    // mysearch(){
    //     return state.search
    // }
  },
  methods: {
    cerca() {
      this.$emit("performSearch", this.search, this.searchType);
      this.search = "";
    },
  },
};
</script>

<style lang="scss">
.myButton {
  height: 40px;
  box-shadow: inset 0px 39px 0px -24px #e67a73;
  background-color: #e4685d;
  border-radius: 15px;
  margin-right: 10px;

  display: inline-block;
  cursor: pointer;
  color: #ffffff;
  font-family: Arial;
  font-size: 15px;
  padding: 6px 15px;
  text-decoration: none;
  text-shadow: 0px 1px 0px #b23e35;
}
.myButton:hover {
  background-color: #eb675e;
}
.myButton:active {
  position: relative;
  top: 1px;
}
.css-input {
  margin-left: 20px;
  margin-right: 10px;
  width: 30%;
  height: 30px;
  padding: 8px;
  font-size: 16px;
  border-width: 0px;
  border-color: #ff2f2f;
  background-color: #ffffff;
  color: #000000;
  border-style: solid;
  border-radius: 2px;
  box-shadow: 0px 0px 5px rgba(66, 66, 66, 0.75);
  text-shadow: 0px 0px 5px rgba(66, 66, 66, 0.75);
}
.css-input:focus {
  outline: none;
}
</style>
