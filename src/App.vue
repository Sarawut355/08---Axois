<template>
  <div id="app">
    <b-navbar type="dark" variant="dark">
      <b-navbar-nav id="nav">
        <router-link to="/">Home</router-link>
      </b-navbar-nav>
      <b-nav-form class="offset-md-10">
        <b-form-input
          size="sm"
          class="mr-sm-2 col-8"
          placeholder="Search"
          v-model="sh"
        ></b-form-input>
        <b-button size="sm" class="my-2 my-sm-0" type="submit" @click="Search()"
          >Search</b-button
        >
      </b-nav-form>
    </b-navbar>
    <router-view :page="page" />
    <!-- <b-button size="sm" @click="Page1()" type="submit">1-100</b-button
    ><b-button size="sm" @click="Page2()" type="submit">101-200</b-button
    ><b-button size="sm" @click="Page3()" type="submit">201-300</b-button> -->
  </div>
</template>
<script>
import axios from "axios";
export default {
  data() {
    return {
      page: 1,
      sh: "",
      animeList: null,
      url: ""
    };
  },
  methods: {
    Search() {
      const router = this.$router;
      for (let i = 0; i <= this.animeList.anime.length; i++) {
        if (this.sh == this.animeList.anime[i].title) {
          alert(this.animeList.anime[i].title);
          router.push({
            path: `/anime/${this.animeList.anime[i].mal_id}`
          });
          break;
        } else if (99 == i) {
          router.push({
            path: `/`
          });
        }
      }
    },
    Page1() {
      this.page = 1;
    },
    Page2() {
      this.page = 2;
    },
    Page3() {
      this.page = 3;
    }
  },
  mounted() {
    this.url = `https://api.jikan.moe/v3/producer/1/${this.page}`;
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
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  background-color: #616161;
}

#nav {
  padding: 10px;
}

#nav a {
  font-weight: bold;
  color: #f3f3f3;
}

#nav a.router-link-exact-active {
  color: #02d9ff;
}
</style>
