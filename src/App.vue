<template>
  <search-bar @search="search"></search-bar>
  <div class="content">
    <filter-list
      v-show="OpenMenu"
      :filters="filters"
      @removeCategories="removeCategories"
      @removeArea="removeArea"
      @removeTags="removeTags"
    ></filter-list>
    <foods-results :search="searchInput" :filters="filters"></foods-results>
  </div>
</template>

<script>
import FoodsResults from "./components/FoodsResults.vue";
import SearchBar from "./components/SearchBar.vue";
import FilterList from "./components/FilterList.vue";
import { computed } from "vue";

export default {
  name: "App",
  components: { SearchBar, FoodsResults, FilterList },
  data() {
    return {
      searchInput: "",
      OpenMenu: true,
      filters: {
        categories: ["Vegetarian", "Food", "Desert"],
        area: ["Stockholm", "Cracow", "Polish"],
        tags: ["Vegetarian", "Soup", "Poland"],
      },
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
    removeCategories(value) {
      const x = this.filters.categories.indexOf(value);
      this.filters.categories.splice(x, 1);
    },
    removeArea(value) {
      const x = this.filters.area.indexOf(value);
      this.filters.area.splice(x, 1);
    },
    removeTags(value) {
      const x = this.filters.tags.indexOf(value);
      this.filters.tags.splice(x, 1);
    },
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@300&display=swap");

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

@media (max-width: 640px) {
  .content {
    height: 100%;
  }
}
</style>

