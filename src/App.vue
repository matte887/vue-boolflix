<template>
  <div id="app">
    <myHeader @searchEvent='filterMovies($event)' />
    <myMain :moviesList='searchedMovies' />
  </div>
</template>

<script>
import myHeader from './components/myHeader.vue';
import myMain from './components/myMain.vue';
import axios from 'axios';

export default {
  name: 'App',
  components: {
    myHeader,
    myMain
  },
  data() {
    return {
      searchedMovies: [],
      researchLink: 'https://api.themoviedb.org/3/search/movie?api_key=e6270ee8d8674f73682b91ddb2f17fe5&query=',
      completeResearchLink: ''
    }
  },
  methods: {
    filterMovies(searchKey) {
      this.createResearchLink(searchKey);
      axios
        .get(this.completeResearchLink)
        .then((resp) => {
          this.searchedMovies = resp.data.results;
        });
    },
    createResearchLink(searchKey) {
      this.completeResearchLink = this.researchLink + searchKey;
    }
  }
}
</script>

<style lang="scss">

</style>
