<template>
  <header>
      <form>
          <input type="text" placeholder="Cerca un film..." v-model="searchKey">
          <button type="button" @click="$emit('searchEvent', searchKey)">Search</button>
      </form>
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

</style>