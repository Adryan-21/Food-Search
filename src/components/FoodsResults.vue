<template>
  <div
    class="container"
    :class="{
      wrap: meals.length % 3 === 1 ? true : false,
      wrap2: meals.length % 3 === 2 ? true : false,
    }"
  >
    <meal-info
      v-for="meal in meals"
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
  props: ["search"],
  data() {
    return {
      meals: [],
      activeId: null,
    };
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
  width: 50vw;
}

.wrap2::after {
  content: "";
  width: 23.5vw;
}
</style>
