<template>
  <div id="app">
    <myHeader @searchEvent="filterMovies($event)" />
    <main>
      <myMain :moviesList="searchedMovies" :TVShowsList="searchedTVShows" />
    </main>
  </div>
</template>

<script>
import myHeader from "./components/myHeader.vue";
import myMain from "./components/myMain.vue";
import axios from "axios";

export default {
  name: "App",
  components: {
    myHeader,
    myMain,
  },
  data() {
    return {
      searchedMovies: [],
      searchedTVShows: [],
      apiKey: "e6270ee8d8674f73682b91ddb2f17fe5",
    };
  },
  methods: {
    filterMovies(searchKey) {
      axios
        .get("https://api.themoviedb.org/3/search/movie", {
          params: {
            api_key: this.apiKey,
            query: searchKey,
          },
        })
        .then((resp) => {
          this.searchedMovies = resp.data.results;
          this.getMovieCredits();
        });
      axios
        .get("https://api.themoviedb.org/3/search/tv", {
          params: {
            api_key: this.apiKey,
            query: searchKey,
          },
        })
        .then((resp) => {
          this.searchedTVShows = resp.data.results;
        });
    },
    getMovieCredits() {
      this.searchedMovies.forEach((movieObj) => {
        axios
          .get(`https://api.themoviedb.org/3/movie/${movieObj.id}/credits?api_key=${this.apiKey}`)
          .then((resp) => {
            movieObj.cast = resp.data.cast.slice(0, 5);
            console.log(movieObj);
          });
      });
    },
  },
};
</script>

<style lang="scss">
@import "./style/common.scss";
@import "./style/variables.scss";
</style>
