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
    // Al click del tasto cerca, questa funzione riceve la chiave di ricerca ed effettua le chiamate API per film e serie TV.
    // I dati ricevuti vengono messi in due array separati. Poi vengono chiamate le funzioni per recuperare gli attori ed i generi.
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
          this.getMoviesGenres();
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
          this.getTVShowCredits();
          this.getTVShowGenres();
        });
    },

    // Questa funzione recupera il cast di ogni film e tronca l'array a 5. L'array viene aggiunto dentro l'oggetto del film.
    getMovieCredits() {
      this.searchedMovies.forEach((movieObj) => {
        axios
          .get(
            `https://api.themoviedb.org/3/movie/${movieObj.id}/credits?api_key=${this.apiKey}`
          )
          .then((resp) => {
            movieObj.cast = resp.data.cast.slice(0, 5);
          });
      });
    },
    // Questa funzione recupera i generi di ogni film sottoforma di array. L'array viene aggiunto dentro l'oggetto del film.
    getMoviesGenres() {
      this.searchedMovies.forEach((movieObj) => {
        axios
          .get(
            `https://api.themoviedb.org/3/movie/${movieObj.id}?api_key=${this.apiKey}`
          )
          .then((resp) => {
            console.log(resp.data.genres);
            movieObj.genres = resp.data.genres;
          });
      });
    },

    // Questa funzione recupera il cast di ogni serieTV e tronca l'array a 5. L'array viene aggiunto dentro l'oggetto della serie TV.
    getTVShowCredits() {
      this.searchedTVShows.forEach((TVShowObj) => {
        axios
          .get(
            `https://api.themoviedb.org/3/tv/${TVShowObj.id}/credits?api_key=${this.apiKey}`
          )
          .then((resp) => {
            TVShowObj.cast = resp.data.cast.slice(0, 5);
          });
      });
    },
    // Questa funzione recupera i generi di ogni serieTV sottoforma di array. L'array viene aggiunto dentro l'oggetto della serie TV.
    getTVShowGenres() {
      this.searchedTVShows.forEach((TVShowObj) => {
        axios
          .get(
            `https://api.themoviedb.org/3/tv/${TVShowObj.id}?api_key=${this.apiKey}`
          )
          .then((resp) => {
            TVShowObj.genres = resp.data.genres;
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
