<template>
  <main>
      <ul>
          <li class="movie-card" v-for="(item, index) in moviesList" :key="index">
              <p>Title: {{item.original_title}}</p>
              <p>Original language: {{item.original_language}}</p>
              <p>Original title: {{item.title}}</p>
              <p>Vote: {{item.vote_average}}/10</p>
          </li>
      </ul>
  </main>
</template>

<script>
export default {
  name: "myMain",
  props: {
    moviesList: Array
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
    }
}
</style>