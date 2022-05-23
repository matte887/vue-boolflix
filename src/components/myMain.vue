<template>
  <main>
    <h2>Movies</h2>
    <ul>
      <li>
        <myCard v-for="(item, index) in moviesList" :key="index" :showData="item" />
      </li>
    </ul>
    <h2>TV Shows</h2>
    <ul>
      <li>
      <myCard v-for="(item, index) in TVShowsList" :key="index" :showData="item" />
      </li>
    </ul>
  </main>
</template>

<script>
import myCard from "./myCard.vue"
export default {
  name: "myMain",
  components: {
    myCard
  },
  props: {
    moviesList: Array,
    TVShowsList: Array,
  },
};
</script>

<style lang="scss" scoped>
ul {
  list-style: none;
}
</style>