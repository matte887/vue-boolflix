<template>
  <header>
      <div class="container d-flex justify-content-between align-items-center">
          <h1>Boolflix</h1>
          <div class="my-research">
              <input class="me-2" type="text" placeholder="Cerca un film..." v-model="searchKey">
              <button @click="$emit('searchEvent', searchKey)">Search</button>
            
            <!-- <div class="filter-movies">
                <label for="choose-movie-genre">Filter movies by genre</label>
                <select name="choose-movie-genre" id="choose-movie-genre" @change="$emit('genreMovieSelected', selectedMovieGenre)" v-model="selectedMovieGenre">
                    <option value="">Tutti</option>
                    <option v-for="genre in moviesGenres" :key="genre.id" :value="genre.id">{{genre.name}}</option>
                </select>
            </div>

            <div class="filter-series">
                <label for="choose-tv-genre">Filter TV Shows by genre</label>
                <select name="choose-tv-genre" id="choose-tv-genre" @change="$emit('genreTVShowSelected', selectedTVShowGenre)" v-model="selectedTVShowGenre">
                    <option value="">Tutti</option>
                    <option v-for="genre in tvShowGenres" :key="genre.id" :value="genre.id">{{genre.name}}</option>
                </select>
            </div> -->

          </div>
      </div>
  </header>
</template>

<script>
// import axios from "axios";
export default {
    name: 'myHeader',
    data() {
        return {
            searchKey: '',
            // selectedMovieGenre: '',
            // selectedTVShowGenre: '',
            // api_key: 'e6270ee8d8674f73682b91ddb2f17fe5',
            // moviesGenres: [],
            // tvShowGenres: []
        }
    },
    // created() {
    //     axios
    //         .get(`https://api.themoviedb.org/3/genre/movie/list?api_key=${this.api_key}`)
    //         .then((resp) => {
    //             this.moviesGenres = resp.data.genres;
    //         });
        
    //     axios
    //         .get(`https://api.themoviedb.org/3/genre/tv/list?api_key=${this.api_key}`)
    //         .then((resp) => {
    //             this.tvShowGenres = resp.data.genres;
    //         });
    // }    
}
</script>

<style lang="scss" scoped>
@import "../style/variables.scss";
header {
    width: 100%;
    background-color: black;
    color: $brand-primary-color;
    .container {
        height: $header-height;
    }
}
</style>