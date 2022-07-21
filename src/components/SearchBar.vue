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
    <div class="wrapper center favorites">
      <button>FAVOURITES</button>
      <font-awesome-icon icon="fa-regular fa-heart" />
    </div>
  </div>
</template>

<script>
export default {
  inject: ["toggle", "open"],
  data() {
    return {
      searchInput: "",
      timer: 0,
    };
  },
  methods: {
    toggleMenu() {
      this.$emit("toggleMenu");
    },
  },
  watch: {
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
  font-size: 1.5vw;
  outline: none;
}
.favorites {
  width: 70%;
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
