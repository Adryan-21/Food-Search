<template>
  <div class="menu">
    <div class="container">
      <h3>Category</h3>
      <div class="filters">
        <div class="filter" v-for="name in filters.categories" :key="name">
          <font-awesome-icon
            icon="fa-solid fa-xmark"
            @click="removeCategories(name)"
          />
          <p>{{ name }}</p>
        </div>
      </div>
    </div>
    <div class="container">
      <h3>Area</h3>
      <div class="filters">
        <div class="filter" v-for="name in filters.area" :key="name">
          <font-awesome-icon
            icon="fa-solid fa-xmark"
            @click="removeArea(name)"
          />
          <p>{{ name }}</p>
        </div>
      </div>
    </div>
    <div class="container">
      <h3>Tags</h3>
      <div class="filters">
        <div class="filter" v-for="name in filters.tags" :key="name">
          <font-awesome-icon
            icon="fa-solid fa-xmark"
            @click="removeTags(name)"
          />
          <p>{{ name }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["filters"],
  methods: {
    removeCategories(value) {
      this.$emit("removeCategories", value);
    },
    removeArea(value) {
      this.$emit("removeArea", value);
    },
    removeTags(value) {
      this.$emit("removeTags", value);
    },
  },
};
</script>

<style scoped>
.menu {
  height: 100%;
  width: 25%;
  background-color: rgb(183, 183, 183);
  display: flex;
  flex-direction: column;
}
.container {
  width: 90%;
  height: 25%;
  display: flex;
  padding-left: 10%;
  margin: 5% 0%;
  display: flex;
  flex-direction: column;
}
.filters {
  width: 80%;
  height: 70%;
  border-radius: 16px;
  border: 1px solid rgb(107, 107, 107);
  margin-top: 5%;
  padding: 5%;
  display: flex;
  flex-wrap: wrap;
}
.container h3 {
  font-size: 1.5vw;
  font-family: "Poppins", sans-serif;
}
.filter {
  min-width: 4vw;
  height: 1vw;
  width: min-content;
  padding: 5%;
  background: rgb(255, 255, 255);
  display: flex;
  justify-content: space-between;
  border-radius: 10px;
  margin-right: 4%;
  margin-bottom: 4%;
  align-items: center;
}
.filter svg {
  cursor: pointer;
}
.filter p {
  margin-left: 5%;
  font-family: "Poppins", sans-serif;
  text-transform: uppercase;
}
</style>
