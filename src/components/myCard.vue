<template>
  <li class="col" @mouseleave="handleLeave" @mouseover="handleHover">
    <div class="movie-card">

      <!-- CARD FRONT: show cover -->
      <div class="card-front" v-if="hover == false">
        <img
          :src="imgLinkRoot + showData.poster_path"
          alt=""
          v-if="showData.poster_path"
        />
        <div class="missing-cover" v-else>
          <p>Missing cover image</p>
          <span class="smile-sad">: (</span>
        </div>
      </div>
      <!-- /CARD FRONT: show cover -->

      <!-- CARD BACK: show info -->
      <div class="card-back hover-info px-3 pt-4" v-if="hover">
        <!-- Titolo dello show -->
        <div class="show-title">
          <h5>
            {{
              showData.original_title ? showData.original_title : showData.name
            }}
          </h5>
        </div>
        <!-- /Titolo dello show -->

        <!-- Lingua originale -->
        <div class="movie-language">
          <span class="fw-bold">Original language:</span>
          {{ showData.original_language }}
          <!-- Mio metodo per bandiere -->
          <!-- <img :src="pickFlag(showData)" alt="" /> -->
          <img
            v-if="languageHasImage()"
            :src="require(`../assets/img/${showData.original_language}.png`)"
            alt=""
          />
          <img
            v-else
            class="globe"
            :src="require('../assets/img/globe.png')"
            alt=""
          />
        </div>
        <!-- /Lingua originale -->

        <!-- Titolo originale (lo mostro solo se diverso dal titolo) -->
        <div
          v-if="
            showData.title !== showData.original_title ||
            showData.original_name !== showData.name
          "
        >
          <span class="fw-bold">Original title:</span>
          <span>
            {{ showData.title ? showData.title : showData.original_name }}
          </span>
        </div>
        <!-- /Titolo originale -->

        <!-- cast -->
        <span class="fw-bold">Cast: </span>
        <ul>
          <li v-for="(item, index) in showData.cast" :key="index">
            {{ item.name }}
          </li>
        </ul>
        <!-- /cast -->

        <!-- genere -->
        <p>
          <span class="fw-bold">Genere: </span>
          <span v-for="(item, index) in showData.genres" :key="index"
            >{{ item.name }},
          </span>
        </p>
        <!-- /genere -->

        <!-- Stringa stelle -->
        <span class="fw-bold">Vote: </span>
        <span
          v-for="(n, index) in convertVote(showData.vote_average)"
          :key="index"
          class="stars"
        >
          <i class="fa-solid fa-star"></i>
        </span>
        <span
          v-for="(n, index) in 5 - convertVote(showData.vote_average)"
          :key="index + 10"
          class="stars"
        >
          <i class="fa-regular fa-star"></i>
        </span>
        <!-- /Stringa stelle -->
      </div>
      <!-- /CARD BACK: show info -->

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
      // Mio metodo per bandiere
      // italianFlag: "assets/img/IT.webp",
      // usaFlag: "assets/img/USA.png",
      // globeFlag: "assets/img/globe.png",
      imgLinkRoot: "http://image.tmdb.org/t/p/w342/",
      hover: false,
      flags: ["en", "it"],
    };
  },
  methods: {
    languageHasImage() {
      return this.flags.includes(this.showData.original_language);
    },

    // Mio metodo per bandiere

    // Funzione che assegna diverse bandiere a diverse sigle.
    // pickFlag(item) {
    //   if (item.original_language === "it") {
    //     return this.italianFlag;
    //   } else if (item.original_language === "en") {
    //     return this.usaFlag;
    //   } else {
    //     return this.globeFlag;
    //   }
    // },

    // Funzione che converte ed arrotonda per eccesso il voto.
    convertVote(vote) {
      const convertedVote = vote / 2;
      const roundedVote = Math.ceil(convertedVote);
      return roundedVote;
    },

    // Funzioni che gestiscono l'hover.
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
@import "../style/variables.scss";
.movie-card {
  height: 100%;
  .card-front {
    height: 100%;
  }
  img {
    height: auto;
    width: 100%;
  }

  .missing-cover {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    height: 100%;
    width: 100%;
    border: 1px solid white;
    .smile-sad {
      writing-mode: tb;
      font-size: 1.5rem;
    }
  }

  .hover-info {
    background-color: black;
    height: 100%;
    .stars {
      color: $star-rating;
    }
  }
  .movie-language {
    img {
      width: 20px;
      height: auto;
      margin-left: 0.2rem;
    }
    .globe {
      filter: invert(1);
    }
  }
}
</style>