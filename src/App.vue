<template>
  <div id="app">
    
    <myHeader @searchEvent="filterMovies($event)"/>

    <main>
      <div class="container d-flex mt-3">
        <!-- Select per filtro film -->
        <div class="filter-movies">
          <label class="me-3" for="choose-movie-genre">Filter movies by genre</label>
          <select
            id="choose-movie-genre"
            v-model="movieGenreSelected"
            class="me-3"
          >
            <option value="">All</option>
            <option v-for="genre in moviesGenres" :key="genre.id" :value="genre.id">
              {{ genre.name }}
            </option>
          </select>
        </div>
        <!-- /Select per filtro film -->
  
        <!-- Select per filtro serie -->
        <div class="filter-series">
          <label class="mx-3" for="choose-tv-genre">Filter TV Shows by genre</label>
          <select
            id="choose-tv-genre"
            v-model="tvShowGenreSelected"
          >
            <option value="">All</option>
            <option v-for="genre in tvShowGenres" :key="genre.id" :value="genre.id">
              {{ genre.name }}
            </option>
          </select>
        </div>
        <!-- /Select per filtro serie -->
      </div>

      
      <myMain
        :moviesList="filterMoviesByGenre"
        :TVShowsList="filterTVShowsByGenre"
      />
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
      apiKey: "e6270ee8d8674f73682b91ddb2f17fe5",
      // Film e serie cercate in base alla chiave di ricerca
      searchedMovies: [],
      searchedTVShows: [],

      // Chiavi per filtri dei generi
      movieGenreSelected: "",
      tvShowGenreSelected: "",

      // Array di generi disponibili
      moviesGenres: [],
      tvShowGenres: [],
    };
  },

  methods: {
    // Al click del tasto cerca, questa funzione riceve la chiave di ricerca ed effettua le chiamate API per film e serie TV.
    // I dati ricevuti vengono messi in due array separati. Poi vengono chiamate le funzioni per recuperare gli attori ed i generi.
    filterMovies(searchKey) {
      const options = {
        params: {
            api_key: this.apiKey,
            query: searchKey,
          }
      };
      axios
        .get("https://api.themoviedb.org/3/search/movie", options)
        .then((resp) => {
          this.searchedMovies = resp.data.results;
          this.getMoviesInfos();
        });

      axios
        .get("https://api.themoviedb.org/3/search/tv", options)
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
          .get(
            `https://api.themoviedb.org/3/tv/${TVShowObj.id}/credits?api_key=${this.apiKey}`
          )
          .then((resp) => {
            TVShowObj.cast = resp.data.cast.slice(0, 5);
          });

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

  computed: {
    // Queste due funzioni controllano i dati relativi alla selezione del filtro. Se questi sono stringhe vuote, le funzioni restituiscono l'array della ricerca originale, se cambiano, le funzioni effettuano la filtrazione sulla base dell'input.
    filterMoviesByGenre() {
      if (this.movieGenreSelected) {
        return this.searchedMovies.filter((thisMovie) => {
          return thisMovie.genre_ids.includes(this.movieGenreSelected);
        });
      } else {
        return this.searchedMovies;
      }
    },
    filterTVShowsByGenre() {
      if (this.tvShowGenreSelected) {
        return this.searchedTVShows.filter((thisTVShow) => {
          return thisTVShow.genre_ids.includes(this.tvShowGenreSelected);
        });
      } else {
        return this.searchedTVShows;
      }
    },
  },
  
  created() {
    // Al caricamento della pagina vengono effettuate due diverse chiamate per richiedere i generi di film e serie tv.
    axios
      .get(
        `https://api.themoviedb.org/3/genre/movie/list?api_key=${this.apiKey}`
      )
      .then((resp) => {
        this.moviesGenres = resp.data.genres;
      });

    axios
      .get(`https://api.themoviedb.org/3/genre/tv/list?api_key=${this.apiKey}`)
      .then((resp) => {
        this.tvShowGenres = resp.data.genres;
      });
  },
};
</script>

<style lang="scss">
@import "./style/common.scss";
@import "./style/variables.scss";
label {
  color: white;
}
</style>