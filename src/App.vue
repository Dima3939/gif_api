<template>
  <v-container>
    <div class="logo">
      <v-img
          max-height="50%"
          max-width="100%"
          src="https://developers.giphy.com/branch/master/static/api-c99e353f761d318322c853c03ebcf21b.gif"
      >
      </v-img>
    </div>
    <gif-search @fetch-gifs="onFetch"/>
    <gif-list :gifs="gifs" />
  </v-container>
</template>

<script>


import GifSearch from "@/components/GifSearch";
import GifList from "@/components/GifList";
export default {
  name: 'App',
  components: {
    GifList,
    GifSearch
  },
  data() {
    return {
      gifs: []
    }
  },
  methods: {
    onFetch(result) {
      this.gifs = result;
    }
  }
}
</script>

<style lang="scss">
  * {
    box-sizing: border-box;
  }
  body {
    padding: 50px;
    background: #000000;  /* fallback for old browsers */
    background: -webkit-linear-gradient(to right, #434343, #000000);  /* Chrome 10-25, Safari 5.1-6 */
    background: linear-gradient(to right, #434343, #000000); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */

  }
  .v-image {
    text-align: center;
    justify-content: center;
  }
</style>
