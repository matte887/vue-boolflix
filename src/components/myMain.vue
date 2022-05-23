<template>
  <main>
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
      italianFlag: "assets/img/IT.webp",
      usaFlag: "assets/img/USA.png",
      globeFlag: "assets/img/globe.png"
    };
  },
  props: {
    moviesList: Array,
  },
  methods: {
    pickFlag(item) {
      if (item.original_language === "it") {
        return this.italianFlag;
      } else if (item.original_language === "en") {
        return this.usaFlag;
      } else {
        return this.globeFlag;
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
      width: 25px;
      height: auto;
      margin-left: 0.2rem;
    }
  }
}
</style>