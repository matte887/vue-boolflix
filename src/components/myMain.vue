<template>
  <div class="container mt-4">
    <h2>Movies</h2>
    <ul class="row row-cols-2 row-cols-md-3 row-cols-lg-4 row-cols-xl-5 gy-3 align-items-stretch">
      <myCard
      v-for="(item, index) in moviesList"
      :key="index"
      :showData="item"
      />
    </ul>
    <h2 class="mt-5">TV Shows</h2>
    <ul class="row row-cols-2 row-cols-md-3 row-cols-lg-4 row-cols-xl-5 gy-3 align-items-stretch">
      <myCard
      v-for="(item, index) in TVShowsList"
      :key="index"
      :showData="item"
      />
    </ul>
  </div>
</template>

<script>
import myCard from "./myCard.vue";
export default {
  name: "myMain",
  components: {
    myCard,
  },
  props: {
    moviesList: Array,
    TVShowsList: Array,
  },
};
</script>

<style lang="scss" scoped>
@import "../style/variables.scss";
.container {
  width: 100%;
  color: white;
  background-color: $background-color;
  ul {
    list-style: none;
    padding: 0;
  }
}
</style>