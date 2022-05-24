<template>
  <li 
    class="col"
    @mouseleave="handleLeave"
    @mouseover="handleHover"
    >

    <div class="movie-card">
      <!-- Show cover -->
      <img
        :src="imgLinkRoot + showData.poster_path"
        alt=""
        v-if="hover == false"
      />
      <!-- /Show cover -->

      <!-- Show info -->
      <div class="hoverInfo" v-if="hover">
        <!-- Titolo dello show -->
        <div class="show-title">
          <h5 v-if="showData.original_title">
            {{ showData.original_title }}
          </h5>
          <h5 v-else>
            {{ showData.name }}
          </h5>
        </div>
        <!-- /Titolo dello show -->

        <!-- Lingua originale -->
        <div class="movie-language">
          <span class="fw-bold">Original language:</span>
          {{ showData.original_language }}
          <img :src="pickFlag(showData)" alt="" />
        </div>
        <!-- /Lingua originale -->

        <!-- Titolo originale -->
        <div>
          <span class="fw-bold">Original title:</span>
          <span v-if="showData.title">
            {{ showData.title }}
          </span>
          <span v-else>
            {{ showData.original_name }}
          </span>
        </div>
        <!-- /Titolo originale -->

        <!-- Stringa stelle -->
        <span class="fw-bold">Vote: </span>
        <span
          v-for="(n, index) in convertVote(showData.vote_average)"
          :key="index"
        >
          <i class="fa-solid fa-star"></i>
        </span>
        <span
          v-for="(n, index) in 5 - convertVote(showData.vote_average)"
          :key="index + 10"
        >
          <i class="fa-regular fa-star"></i>
        </span>
        <!-- /Stringa stelle -->
      </div>
      <!-- /Show info -->
    </div>
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
      imgLinkRoot: "http://image.tmdb.org/t/p/w342/",
      hover: false,
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
    handleHover() {
      this.hover = true;
    },
    handleLeave() {
      this.hover = false;
    },
  },
};
</script>

<style lang="scss" scoped>
.col {
  .movie-card {
    height: 100%;
    .movie-language img {
      width: 25px;
      height: auto;
      margin-left: 0.2rem;
    }
    img {
      height: auto;
      width: 100%;
    }
  }
}
</style>