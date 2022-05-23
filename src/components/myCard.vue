<template>
    <li class="movie-card">
      <img :src="imgLinkRoot + showData.poster_path" alt="" />
      <p>Title: {{ showData.original_title }}</p>
      <div class="movie-language">
        Original language: {{ showData.original_language }}
        <img :src="pickFlag(showData)" alt="" />
      </div>
      <p>Original title: {{ showData.title }}</p>
      <span>Vote:</span>
      <span v-for="(n, index) in convertVote(showData.vote_average)" :key="index"><i class="fa-solid fa-star"></i></span>
      <span v-for="(n, index) in 5 - convertVote(showData.vote_average)" :key="index + 10"><i class="fa-regular fa-star"></i></span>
    </li>
</template>

<script>
export default {
  name: "myCard",
  props: {
    showData: Object,
  },
  data() {
    return {
      italianFlag: "assets/img/IT.webp",
      usaFlag: "assets/img/USA.png",
      globeFlag: "assets/img/globe.png",
      imgLinkRoot: "http://image.tmdb.org/t/p/w500/",
      stars: "",
    };
  },
  methods: {
    pickFlag(item) {
      if (item.original_language === "it") {
        return this.italianFlag;
      } else if (item.original_language === "en") {
        return this.usaFlag;
      } else {
        return this.globeFlag;
      }
    },
    convertVote(vote) {
      const convertedVote = vote / 2;
      const roundedVote = Math.ceil(convertedVote);
      return roundedVote;
    },
  },
};
</script>

<style lang="scss" scoped>
.movie-card {
  border: 1px solid black;
  display: inline-block;
  margin: 1rem;
  padding: 1rem;
  .movie-language img {
    width: 25px;
    height: auto;
    margin-left: 0.2rem;
  }
  img {
    height: 200px;
    width: auto;
  }
}
</style>