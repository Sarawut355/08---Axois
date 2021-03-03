<template>
  <div class="container col-10" style="height: 60rem">
    {{ id }}
    <div class="row">
      <div class="col-3">
        <b-img
          thumbnail
          fluid
          :src="animeList.anime[id].image_url"
          alt="Fluid image"
          style="height: 40rem; width: 30rem"
        ></b-img>
        <b class="Name-Anime">{{ animeList.anime[id].title }}</b>
        <div class="row Genres">
          <b>Genres:</b>
          <b
            v-for="(item, index) in animeList.anime[id].genres"
            :key="index"
            class="offset-md-1"
          >
            {{ item.name }}
          </b>
        </div>
      </div>
      <div class="col-8">
        <p class="Trailer-Anime">
          {{ animeList.anime[id].synopsis }}
        </p>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      id: 0,
      animeList: null,
      url: "https://api.jikan.moe/v3/producer/1/1"
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
    this.id = this.$route.params.id;
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
