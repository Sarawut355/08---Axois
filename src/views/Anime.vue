<template>
  <div class="container col-10" style="height: 60rem">
    <div class="row">
      <div class="col-3">
        <b-img
          thumbnail
          fluid
          :src="animeList.image_url"
          alt="Fluid image"
          style="height: 40rem; width: 30rem"
        ></b-img>
        <b class="Name-Anime"
          >{{ animeList.title }} ( {{ animeList.title_japanese }} )</b
        >
        <div class="row Genres">
          <b>Genres:</b>
          <b
            v-for="(item, index) in animeList.genres"
            :key="index"
            class="offset-md-1"
          >
            {{ item.name }}
          </b>
        </div>
      </div>
      <div class="col-8">
        <p class="Trailer-Anime">
          {{ animeList.synopsis }}
        </p>
        <iframe width="420" height="345" :src="animeList.trailer_url"> </iframe>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      animeList: null,
      url: `https://api.jikan.moe/v3/anime/${this.$route.params.id}`
    };
  },
  mounted() {
    axios
      .get(this.url)
      .then(result => {
        this.animeList = result.data;
      })
      .catch(err => {
        console.log(err);
        alert(err);
      });
  }
};
</script>

<style>
.Name-Anime {
  color: #3333ff;
  font-size: 40px;
  text-shadow: 2px 2px #00ffff;
}
.Trailer-Anime {
  color: #ffffff;
  font-size: 24px;
}
.Genres {
  color: #00ffff;
  font-size: 18px;
}
</style>
