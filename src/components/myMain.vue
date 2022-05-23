<template>
  <main>
    <h2>Movies</h2>
    <ul>
      <li class="movie-card" v-for="(item, index) in moviesList" :key="index">
        <img :src="imgLinkRoot + item.poster_path" alt="" />
        <p>Title: {{ item.original_title }}</p>
        <div class="movie-language">
          Original language: {{ item.original_language }}
          <img :src="pickFlag(item)" alt="" />
        </div>
        <p>Original title: {{ item.title }}</p>
        <p>Vote: {{ convertVote(item.vote_average) }}</p>
      </li>
    </ul>
    <h2>TV Shows</h2>
    <ul>
      <li class="movie-card" v-for="(item, index) in TVShowsList" :key="index">
        <p>Title: {{ item.name }}</p>
        <div class="movie-language">
          Original language: {{ item.original_language }}
          <img :src="pickFlag(item)" alt="" />
        </div>
        <p>Original title: {{ item.name }}</p>
        <p>Vote: {{ convertVote(item.vote_average) }}</p>
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
      globeFlag: "assets/img/globe.png",
      imgLinkRoot: "http://image.tmdb.org/t/p/w500/",
    };
  },
  props: {
    moviesList: Array,
    TVShowsList: Array,
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
    convertVote(vote) {
      console.log(vote);
    }
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
    img {
      height: 200px;
      width: auto;
    }
  }
}
</style>