<template>
  <search-bar @search="search"></search-bar>
  <div class="content">
    <div class="menu" v-show="OpenMenu"></div>
    <foods-results :search="searchInput"></foods-results>
  </div>
</template>

<script>
import FoodsResults from "./components/FoodsResults.vue";
import SearchBar from "./components/SearchBar.vue";
import { computed } from "vue";

export default {
  name: "App",
  components: { SearchBar, FoodsResults },
  data() {
    return {
      searchInput: "",
      OpenMenu: true,
    };
  },
  provide() {
    return {
      open: computed(() => this.OpenMenu),
      toggle: this.toggleMenu,
    };
  },
  methods: {
    search(val) {
      this.searchInput = val;
    },
    toggleMenu() {
      this.OpenMenu = !this.OpenMenu;
    },
  },
};
</script>

<style>
* {
  margin: 0;
}

#app {
  width: 100%;
  height: 100vh;
  background: white;
  overflow: hidden;
}

.content {
  height: 92.5%;
  width: 100%;
  display: flex;
  background-color: rgb(250, 250, 250);
}
.menu {
  height: 100%;
  width: 20%;
  background-color: rgb(183, 183, 183);
}
</style>

