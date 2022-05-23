<template>
  <main>
    <!-- <img src="../assets/img/IT.webp" alt=""> -->
    <ul>
      <li class="movie-card" v-for="(item, index) in moviesList" :key="index">
        <p>Title: {{ item.original_title }}</p>
        <div class="movie-language">
          Original language: {{ item.original_language }}
          <img :src="pickFlag(item)" alt="" />
        </div>
        <p>Original title: {{ item.title }}</p>
        <p>Vote: {{ item.vote_average }}/10</p>
      </li>
    </ul>
  </main>
</template>

<script>
export default {
  name: "myMain",
  data() {
    return {
      italianFlag: "../assets/img/IT.webp",
    };
  },
  props: {
    moviesList: Array,
  },
  methods: {
    pickFlag(item) {
      if (item.original_language === "it") {
        return this.italianFlag;
      }
    },
  },
};
</script>

<style lang="scss" scoped>
ul {
  list-style: none;
  .movie-card {
    border: 1px solid black;
    display: inline-block;
    margin: 1rem;
    padding: 1rem;
    .movie-language img {
      width: 20px;
      margin-left: 0.2rem;
    }
  }
}
</style>