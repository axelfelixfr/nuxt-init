<template lang="html">
  <div class="container">
    <header>
      <h1 class="title">{{album.title}}</h1>
    <nuxt-link to="/">Regresar</nuxt-link>
    </header>
    <div class="columns is-multiline">
      <div class="column is-one-quarter" v-for="photo in photos" :key="photo.id">
        <img :src="photo.url" :alt="photo.title">
      </div>
    </div>
  </div>
</template>
<script>
import axios from "axios";
import router from "vue-router";
import env from "../../config/env";
export default {
  name: "AlbumIndivPage",
  data() {
    return {
      album: {},
      photos: []
    };
  },
  created: async function () {
    // let albumId = this.$route.params.id;
    // console.log(albumId);
    let albumResponse = await axios.get(
      `${env.endpoint}/albums/${this.$route.params.id}`
    );
    this.album = albumResponse.data;
    let photoResponse = await axios.get(
      `${env.endpoint}/albums/${this.$route.params.id}/photos`
    );
    this.photos = photoResponse.data;
  }
};
</script>
<style lang="css" scoped>
.container {
  text-align: center;
}
</style>