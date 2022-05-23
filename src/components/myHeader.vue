<template>
  <header>
      <div class="container d-flex justify-content-between align-items-center">
          <h1>Boolflix</h1>
          <form>
              <input class="me-2" type="text" placeholder="Cerca un film..." v-model="searchKey">
              <button type="button" @click="$emit('searchEvent', searchKey)">Search</button>
          </form>
      </div>
  </header>
</template>

<script>
export default {
    name: 'myHeader',
    data() {
        return {
            searchKey: ''
        }
    },
    methods: {
        searchMovie() {
            return console.log('ciao');
        }
    }
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