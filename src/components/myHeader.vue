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
        <button @click="sendSearchEvent()">Search</button>
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
  methods: {
    // Con questa funzione inviamo l'evento al padre solo se searchKey è una stringa non vuota.
    sendSearchEvent() {
      if (this.searchKey.trim()) {
        return this.$emit('searchEvent', this.searchKey)
      }
    }
  }
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
    input {
      border: none;
    }
    button {
      border: none;
    }
  }
}
</style>