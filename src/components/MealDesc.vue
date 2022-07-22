<template>
  <div class="info" :class="{ big: !Opened }">
    <iframe :src="loadLink" frameborder="0"></iframe>
    <div class="desc">
      <h3>Instruction</h3>
      <p>{{ instructions }}</p>
      <h3>Ingredients + Measure</h3>
      <ul>
        <li v-for="ingredient in ingredients" :key="ingredient">
          {{ ingredient.ingredient }} - {{ ingredient.measure }}
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  props: ["id", "ingredients", "instructions", "link", "open"],
  data() {
    return {
      Opened: this.open,
    };
  },
  computed: {
    loadLink() {
      const x = this.link.indexOf("=") + 1;
      const id = this.link.substring(x, this.link.lenght);
      return "https://www.youtube.com/embed/" + id;
    },
  },
};
</script>

<style scoped>
.info {
  position: relative;
  width: 72.75vw;
  height: max-content;
  border: 2px solid rgb(181, 181, 181);
  border-radius: 18px;
  display: flex;
}
.info.big {
  width: 91vw;
}

.info iframe {
  border-radius: 16px 0 0 16px;
  width: 35%;
}

.desc {
  width: 62%;
  padding: 2%;
}
.desc p {
  margin-bottom: 2%;
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen,
    Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
  line-height: 1.2vw;
  color: rgb(150, 150, 150);
  font-size: 1vw;
}
.desc h3 {
  font-size: 2rem;
  color: rgb(107, 107, 107);
  margin-bottom: 2%;
  font-family: "Poppins", sans-serif;
  font-size: 1.5vw;
}
.desc ul {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr 1fr;
  font-size: 1vw;
}
.desc li {
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen,
    Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
  line-height: 1vw;
  color: rgb(150, 150, 150);
  text-transform: uppercase;
  width: 90%;
}
@media (max-width: 640px) {
  .info {
    width: 75.75vw;
    border-radius: 14px;
    display: flex;
    flex-direction: column;
  }
  .info iframe {
    border-radius: 12px 12px 0 0;
    width: 100%;
  }
  .info .desc {
    width: 95%;
  }
  .desc h3 {
    font-size: 3vw;
  }
  .desc p {
    font-size: 2vw;
    line-height: 2vw;
  }
  .desc ul {
    grid-template-columns: 1fr 1fr 1fr;
    font-size: 1.75vw;
    padding-left: 2vw;
  }
  .desc li {
    line-height: 2.5vw;
    width: 85%;
  }
  .info.big {
    width: 94.5vw;
  }
}
</style>
