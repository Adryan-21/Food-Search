<template>
  <div
    class="container"
    :class="{
      wrap:
        filterFood.length % 3 === 1 || filterFood.length == 1 ? true : false,
      wrap2:
        filterFood.length !== 1 &&
        (filterFood.length % 3 === 2 || filterFood.length == 2)
          ? true
          : false,
    }"
  >
    <meal-info
      v-for="meal in filterFood"
      :key="meal.idMeal"
      :meal="meal"
      :activeId="activeId"
      @activeCard="activeCard(meal.idMeal)"
    ></meal-info>
  </div>
</template>

<script>
import MealInfo from "./MealInfo.vue";
export default {
  components: { MealInfo },
  props: ["search", "filters"],
  data() {
    return {
      meals: [],
      activeId: null,
    };
  },
  computed: {
    filterFood() {
      return this.meals.filter((e) => {
        return this.filters.area.length !== 0
          ? this.filters.area.some((v) => e.strArea.includes(v))
          : this.meals && this.filters.categories.length !== 0
          ? this.filters.categories.some((v) => e.strCategory.includes(v))
          : this.meals && this.filters.categories.length !== 0
          ? this.filters.tags.some((v) =>
              e.strTags !== null ? e.strTags.includes(v) : this.meals
            )
          : this.meals;
      });
    },
  },
  mounted() {
    this.loadMeals();
  },
  watch: {
    search() {
      this.activeId = null;
      this.loadMeals();
    },
  },
  methods: {
    activeCard(val) {
      if (val === this.activeId) {
        this.activeId = null;
      } else {
        this.activeId = val;
      }
    },
    loadMeals() {
      fetch(
        "https://www.themealdb.com/api/json/v1/1/search.php?s=" +
          (this.search ? this.search : "Soup")
      )
        .then((result) => {
          return result.json();
        })
        .then((data) => {
          this.meals = data.meals;
        });
    },
  },
};
</script>

<style scoped>
.container {
  width: 100%;
  height: 97%;
  display: flex;
  justify-content: space-evenly;
  padding-top: 3%;
  flex-wrap: wrap;
  overflow-y: scroll;
}
.wrap::after {
  content: "";
  width: 47.5vw;
}

.wrap2::after {
  content: "";
  width: 23.5vw;
}
@media (max-width: 640px) {
  .container {
    height: 93%;
  }
  .wrap::after {
    content: "";
    width: 36.5vw;
  }

  .wrap2::after {
    content: "";
    width: 23.5vw;
  }
}
</style>
