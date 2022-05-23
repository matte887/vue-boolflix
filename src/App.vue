<template>
  <div id="app">
    <myHeader @searchEvent="filterMovies($event)" />
    <myMain :moviesList="searchedMovies" :TVShowsList="searchedTVShows" />
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
      researchLink:
        "https://api.themoviedb.org/3/search/movie?api_key=e6270ee8d8674f73682b91ddb2f17fe5&query=",
      tvShowLink:
        "https://api.themoviedb.org/3/search/tv?api_key=e99307154c6dfb0b4750f6603256716d&query=",
      completeResearchLink: "",
      completeTVShowLink: "",
    };
  },
  methods: {
    filterMovies(searchKey) {
      this.createResearchLink(searchKey);
      axios.get(this.completeResearchLink).then((resp) => {
        this.searchedMovies = resp.data.results;
        this.searchedMovies.forEach(element => {
          this.searchedMovies.push(element)
        });
      });
      axios.get(this.completeTVShowLink).then((resp) => {
        this.searchedTVShows = resp.data.results;
        this.searchedMovies.forEach(element => {
          this.searchedMovies.push(element)
        });
      });
    },
    createResearchLink(searchKey) {
      this.completeResearchLink = this.researchLink + searchKey;
      this.completeTVShowLink = this.tvShowLink + searchKey;
    },
  },
};
</script>

<style lang="scss">
</style>
