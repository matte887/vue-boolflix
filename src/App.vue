<template>
  <myHeader @searchEvent='filterMovies($event)' />
</template>

<script>
import myHeader from './components/myHeader.vue'

export default {
  name: 'App',
  components: {
    myHeader
  },
  methods: {
    filterMovies(searchKey) {
      console.log(searchKey);
    }
  }
}
</script>

<style lang="scss">

</style>
