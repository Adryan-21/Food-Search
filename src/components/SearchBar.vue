<template>
  <div class="navigator">
    <div class="wrapper">
      <button class="icon-menu">
        <font-awesome-icon
          icon="fa-solid fa-bars"
          @click="toggle"
        ></font-awesome-icon>
      </button>
    </div>
    <div class="wrapper center search">
      <font-awesome-icon icon="fa-solid fa-magnifying-glass" />
      <input type="text" placeholder="SEARCH" v-model="searchInput" />
    </div>
    <div
      class="wrapper center favorites"
      :class="{ active: showfav }"
      @mouseover="showfav = true"
      @mouseout="showfav = false"
    >
      <div class="container">
        <button>FAVOURITES</button>
        <font-awesome-icon icon="fa-regular fa-heart" />
      </div>
      <div
        class="favorite"
        v-show="showfav"
        @mouseover="showfav = true"
        @mouseout="showfav = false"
      >
        <div
          v-for="meal in favourites"
          :key="meal.id"
          class="item"
          @click="selectFavMeal(meal.name)"
        >
          <div :style="'background-image: url(' + meal.img + ')'" class="img" />
          <p>{{ meal.name }}</p>
        </div>
        <p v-if="favourites.length === 0">Empty</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  inject: ["toggle", "open"],
  data() {
    return {
      searchInput: "",
      showfav: false,
      timer: 0,
      favourites: [],
    };
  },
  mounted() {
    this.favourites =
      localStorage.favoriteMeals !== undefined
        ? JSON.parse(localStorage.favoriteMeals)
        : [];
  },
  methods: {
    toggleMenu() {
      this.$emit("toggleMenu");
    },
    selectFavMeal(name) {
      this.searchInput = name;
      this.$emit("search", name);
    },
  },
  watch: {
    showfav() {
      this.favourites =
        localStorage.favoriteMeals !== undefined
          ? JSON.parse(localStorage.favoriteMeals)
          : [];
    },
    searchInput() {
      if (this.timer) {
        clearTimeout(this.timer);
        this.timer = null;
      }
      this.timer = setTimeout(() => {
        this.$emit("search", this.searchInput);
      }, 500);
    },
  },
};
</script>

<style scoped>
.navigator {
  width: 100%;
  height: clamp(7.5%, 2vw, 11vh);
  background: rgb(255, 255, 141);
  display: grid;
  grid-template-columns: 0.75fr 2fr 1fr;
  grid-template-rows: 1fr;
}
.wrapper {
  display: flex;
  align-items: center;
}
.center {
  justify-self: center;
  align-self: center;
  border: 1px solid rgb(181, 181, 181);
  height: 50%;
  border-radius: 8px;
}

.search {
  width: 90%;
}
.search svg {
  margin: 0 2%;
  color: rgb(70, 70, 70);
}
.search input {
  background-color: transparent;
  border: 0;
  width: 90%;
  height: 70%;
  font-size: 1.25vw;
  outline: none;
  color: rgb(70, 70, 70);
}
.favorites {
  width: 70%;
  display: flex;
  flex-direction: column;
  color: rgb(70, 70, 70);
}
.favorites.active {
  background-color: white;
  border-radius: 8px 8px 0 0;
}

.favorites .container {
  display: flex;
  height: 100%;
  gap: 75%;
  align-items: center;
}
.favorites .favorite {
  position: absolute;
  top: 5vh;
  background-color: white;
  width: 16.6vw;
  border: 1px solid rgb(181, 181, 181);
  border-top: 0;
  padding: 1vw;
  border-radius: 0px 0px 8px 8px;
  z-index: 5;
}

.favorites button {
  border: 0;
  background-color: transparent;
  color: rgb(70, 70, 70);
}

.favorites svg {
  font-size: 1.2vw;
  color: rgb(70, 70, 70);
}
.item {
  display: flex;
  width: 12vw;
  height: 3vw;
  align-items: center;
  font-family: "Poppins", sans-serif;
  gap: 1vw;
  padding-left: 2vw;
  cursor: pointer;
}
.item .img {
  width: 35%;
  height: 75%;
  background-size: 100%;
  background-position: 100% 25%;
}
.favorite p {
  font-family: "Poppins", sans-serif;
}

.icon-menu {
  background-color: transparent;
  border: 0;
  font-size: clamp(1vh, 2.5vw, 3vw);
  margin-left: 2.5%;
}
.icon-menu:hover {
  cursor: pointer;
}
</style>
