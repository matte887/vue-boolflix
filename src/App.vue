<template>
  <div id="app">
    <myHeader
      @searchEvent="filterMovies($event)"
      @genreMovieSelected="receiveMovieGenre($event)"
      @genreTVSelected="filterTVByGenre($event)"
    />
    <main>
      <myMain :moviesList="filterMoviesByGenre" :TVShowsList="searchedTVShows" />
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
      movieGenreSelected: '',
      filteredMoviesArray: []
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
          this.getMoviesInfos();
          console.log(this.searchedMovies);
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
          this.getTVShowsInfos();
        });
    },

    // Questa funzione recupera il cast ed i generi di ogni film. Gli array ottenuti vengono aggiunti come nuove proprietà dell'oggetto del film.
    getMoviesInfos() {
      this.searchedMovies.forEach((movieObj) => {
        axios
          .get(
            `https://api.themoviedb.org/3/movie/${movieObj.id}/credits?api_key=${this.apiKey}`
          )
          .then((resp) => {
            movieObj.cast = resp.data.cast.slice(0, 5);
          });

        axios
          .get(
            `https://api.themoviedb.org/3/movie/${movieObj.id}?api_key=${this.apiKey}`
          )
          .then((resp) => {
            movieObj.genres = resp.data.genres;
          });
      });
    },

    // Questa funzione recupera il cast ed i generi di ogni serieTV e tronca l'array a 5. Gli array ottenuti vengono aggiunti come nuove proprietà dell'oggetto delle serie.
    getTVShowsInfos() {
      this.searchedTVShows.forEach((TVShowObj) => {
        axios
          .get(`https://api.themoviedb.org/3/tv/${TVShowObj.id}/credits?api_key=${this.apiKey}`)
          .then((resp) => {
            TVShowObj.cast = resp.data.cast.slice(0, 5);
          });

        axios
          .get(`https://api.themoviedb.org/3/tv/${TVShowObj.id}?api_key=${this.apiKey}`)
          .then((resp) => {
            TVShowObj.genres = resp.data.genres;
          });
      });
    },
    receiveMovieGenre(genre) {
      this.movieGenreSelected = genre;
      console.log(this.movieGenreSelected);
      // this.filterMoviesByGenre();
    },
    // filterMoviesByGenre() {
    //   const filteredMovies = this.searchedMovies.filter((thisMovie) => {
    //     return thisMovie.genre_ids.includes(this.movieGenreSelected);
    //   });
    //   console.log(filteredMovies);
    //   this.filteredMoviesArray = filteredMovies;
    //   return filteredMovies;
    // },
    // filterMoviesByGenre() {
    //   if (this.movieGenreSelected) {
    //     return this.searchedMovies.filter((thisMovie) => {
    //       return thisMovie.genre_ids.includes(this.movieGenreSelected);
    //     });
    //   } else {
    //     return this.searchedMovies;
    //   }
  },
  computed: {
    filterMoviesByGenre() {
      if (this.movieGenreSelected) {
        return this.searchedMovies.filter((thisMovie) => {
          return thisMovie.genre_ids.includes(this.movieGenreSelected);
        });
      } else {
        return this.searchedMovies;
      }
    }
  }
};
</script>

<style lang="scss">
@import "./style/common.scss";
@import "./style/variables.scss";
</style>
