<template>
  <div class="wrapper" :class="active">
    <div
      class="meal"
      :class="active"
      :style="'background-image: url(' + meal.strMealThumb + ')'"
      @click.self="activeCard"
    >
      <div
        class="favorite"
        @click.self="activeCard"
        :class="{ isfavorite: isFavorite }"
      >
        <font-awesome-icon
          icon="fa-regular fa-heart"
          @click.self="addToFavorite"
        />
      </div>
      <div class="name" @click.self="activeCard">
        {{ meal.strMeal }}
      </div>
    </div>
    <meal-desc
      v-show="meal.idMeal === activeId"
      :id="meal.idMeal"
      :instructions="meal.strInstructions"
      :ingredients="ingredients"
      :link="meal.strYoutube"
      :open="open"
    ></meal-desc>
  </div>
</template>

<script>
import MealDesc from "./MealDesc.vue";
export default {
  inject: ["open"],
  components: { MealDesc },
  props: ["meal", "activeId"],
  data() {
    return {
      sizeInfo: 0,
      favoriteMeals: [],
    };
  },
  mounted() {
    this.favoriteMeals =
      localStorage.favoriteMeals !== undefined
        ? JSON.parse(localStorage.favoriteMeals)
        : [];
  },
  computed: {
    active() {
      if (this.meal.idMeal !== this.activeId && this.activeId !== null) {
        return "inactive";
      } else if (this.meal.idMeal === this.activeId) {
        return "active";
      } else {
        return null;
      }
    },
    isFavorite() {
      return this.favoriteMeals.some((v) => v.id === this.meal.idMeal);
    },
    ingredients() {
      let ingredients = [];
      this.meal.strIngredient1 !== ""
        ? ingredients.push({
            ingredient: this.meal.strIngredient1,
            measure: this.meal.strMeasure1,
          })
        : null;
      this.meal.strIngredient2 !== ""
        ? ingredients.push({
            ingredient: this.meal.strIngredient2,
            measure: this.meal.strMeasure2,
          })
        : null;
      this.meal.strIngredient3 !== ""
        ? ingredients.push({
            ingredient: this.meal.strIngredient3,
            measure: this.meal.strMeasure3,
          })
        : null;

      this.meal.strIngredient4 !== ""
        ? ingredients.push({
            ingredient: this.meal.strIngredient4,
            measure: this.meal.strMeasure4,
          })
        : null;

      this.meal.strIngredient5 !== ""
        ? ingredients.push({
            ingredient: this.meal.strIngredient5,
            measure: this.meal.strMeasure5,
          })
        : null;

      this.meal.strIngredient6 !== ""
        ? ingredients.push({
            ingredient: this.meal.strIngredient6,
            measure: this.meal.strMeasure6,
          })
        : null;

      this.meal.strIngredient7 !== ""
        ? ingredients.push({
            ingredient: this.meal.strIngredient7,
            measure: this.meal.strMeasure7,
          })
        : null;

      this.meal.strIngredient8 !== ""
        ? ingredients.push({
            ingredient: this.meal.strIngredient8,
            measure: this.meal.strMeasure8,
          })
        : null;

      this.meal.strIngredient9 !== ""
        ? ingredients.push({
            ingredient: this.meal.strIngredient9,
            measure: this.meal.strMeasure9,
          })
        : null;

      this.meal.strIngredient10 !== ""
        ? ingredients.push({
            ingredient: this.meal.strIngredient10,
            measure: this.meal.strMeasure10,
          })
        : null;

      this.meal.strIngredient11 !== ""
        ? ingredients.push({
            ingredient: this.meal.strIngredient11,
            measure: this.meal.strMeasure11,
          })
        : null;

      this.meal.strIngredient12 !== ""
        ? ingredients.push({
            ingredient: this.meal.strIngredient12,
            measure: this.meal.strMeasure12,
          })
        : null;

      this.meal.strIngredient13 !== ""
        ? ingredients.push({
            ingredient: this.meal.strIngredient13,
            measure: this.meal.strMeasure13,
          })
        : null;

      this.meal.strIngredient14 !== ""
        ? ingredients.push({
            ingredient: this.meal.strIngredient14,
            measure: this.meal.strMeasure14,
          })
        : null;

      this.meal.strIngredient15 !== ""
        ? ingredients.push({
            ingredient: this.meal.strIngredient15,
            measure: this.meal.strMeasure15,
          })
        : null;

      this.meal.strIngredient16 !== ""
        ? ingredients.push({
            ingredient: this.meal.strIngredient16,
            measure: this.meal.strMeasure16,
          })
        : null;

      this.meal.strIngredient17 !== ""
        ? ingredients.push({
            ingredient: this.meal.strIngredient17,
            measure: this.meal.strMeasure17,
          })
        : null;

      this.meal.strIngredient18 !== ""
        ? ingredients.push({
            ingredient: this.meal.strIngredient18,
            measure: this.meal.strMeasure18,
          })
        : null;

      this.meal.strIngredient19 !== ""
        ? ingredients.push({
            ingredient: this.meal.strIngredient19,
            measure: this.meal.strMeasure19,
          })
        : null;

      this.meal.strIngredient20 !== ""
        ? ingredients.push({
            ingredient: this.meal.strIngredient20,
            measure: this.meal.strMeasure20,
          })
        : null;

      return ingredients;
    },
  },
  methods: {
    activeCard() {
      this.$emit("activeCard", this.activeId);
    },
    addToFavorite() {
      let x =
        localStorage.favoriteMeals !== undefined
          ? JSON.parse(localStorage.favoriteMeals)
          : [];
      if (!x.some((v) => v.id === this.meal.idMeal)) {
        x.push({
          id: this.meal.idMeal,
          name: this.meal.strMeal,
          img: this.meal.strMealThumb,
        });
        localStorage.favoriteMeals = JSON.stringify(x);
        this.favoriteMeals = x;
      } else {
        const index = x.findIndex((o) => {
          return o.id === this.meal.idMeal;
        });
        x.splice(index, index + 1);
        localStorage.favoriteMeals = JSON.stringify(x);
        this.favoriteMeals = x;
      }
    },
  },
};
</script>

<style scoped>
.meal {
  width: 100%;
  height: 22vw;
  overflow: hidden;
  border: 2px solid rgb(181, 181, 181);
  border-radius: 8px;
  transition: opacity 0.5s;
  background-size: 100%;
  display: flex;
  flex-direction: column;
  justify-content: flex-end;
}
.name {
  height: 15%;
  background-color: white;
  display: flex;
  align-items: center;
  justify-content: center;
  color: rgb(181, 181, 181);
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen,
    Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
  text-transform: uppercase;
  font-size: 1.1vw;
}
.favorite {
  display: flex;
  height: 15%;
  color: white;
  font-size: 2vw;
  padding-right: 5%;
  justify-content: right;
}
.favorite.isfavorite {
  color: rgb(255, 255, 141);
}
.favorite svg:hover {
  cursor: pointer;
}

.active {
  margin-bottom: 5%;
}

.inactive {
  opacity: 0.5;
}

img {
  width: 100%;
}
.wrapper {
  width: 28%;
  margin-bottom: 3%;
  height: 22vw;
}

.wrapper.active {
  height: max-content;
}

.wrapper:nth-child(3n + 2) .info,
.wrapper:nth-child(2) .info {
  left: -25vw;
}
.wrapper:nth-child(3n + 2) .info.big,
.wrapper:nth-child(2) .info.big {
  left: -31.5vw;
}
.wrapper:nth-child(3n + 3) .info {
  left: -50.5vw;
}
.wrapper:nth-child(3n + 3) .info.big {
  left: -63.5vw;
}
</style>
