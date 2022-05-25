<template>
<header>
    <div class="container d-flex justify-content-between align-items-center">
      <h1>Boolflix</h1>
      <div class="my-research">
        <input
          class="me-2"
          type="text"
          placeholder="Search a movie..."
          v-model="searchKey"
        />
        <button @click="$emit('searchEvent', searchKey)">Search</button>
      </div>
    </div>
</header>
</template>

<script>
export default {
  name: "myHeader",
  data() {
    return {
      searchKey: "",
    };
  },
};
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