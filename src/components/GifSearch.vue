<template>
  <v-container>
    <input placeholder="Поиск gif" v-model="keyword" @input="onInput">
    <div class="firstLook">
      <v-row v-show="!keyword">
        <v-col
            v-for="n in 9"
            :key="n"
            class="d-flex child-flex"
            cols="4"
        >
          <v-img
              :src="`https://picsum.photos/500/300?image=${n * 5 + 10}`"
              :lazy-src="`https://picsum.photos/10/6?image=${n * 5 + 10}`"
              aspect-ratio="1"
              class="grey lighten-2"
          >
            <template v-slot:placeholder>
              <v-row
                  class="fill-height ma-0"
                  align="center"
                  justify="center"
              >
                <v-progress-circular
                    indeterminate
                    color="grey lighten-5"
                ></v-progress-circular>
              </v-row>
            </template>
          </v-img>
        </v-col>
      </v-row>
    </div>
  </v-container>
</template>

<script>
export default {
  name: "GifSearch",
  data(){
    return {
      keyword: '',
      timeout: null,
    }
  },
  methods: {
    onInput() {
      clearTimeout(this.timeout);
      this.timeout = setTimeout(() => {
        this.search();
      }, 500)
    },
    search() {
      fetch(`https://api.giphy.com/v1/gifs/search?api_key=F6rui6fPTuMxBuPHDSX6wuNuoojoLfh2&q=${this.keyword}`)
          .then(response => response.json())
          .then(result => {
            console.log(result);
            this.$emit('fetch-gifs', result.data);
          })
    }
  }
}
</script>

<style scoped>
  input {
    padding: 10px 16px;
    border-radius: 4px;
    font-size: 18px;
    outline: 0;
    border: 2px solid black;
    display: block;
    width: 100%;
    margin-top: 20px;
    margin-bottom: 20px;
    color: white;
    background: #232526;  /* fallback for old browsers */
    background: -webkit-linear-gradient(to right, #414345, #232526);  /* Chrome 10-25, Safari 5.1-6 */
    background: linear-gradient(to right, #414345, #232526); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */

  }
  input:focus {
    background: #141E30;  /* fallback for old browsers */
    background: -webkit-linear-gradient(to right, #243B55, #141E30);  /* Chrome 10-25, Safari 5.1-6 */
    background: linear-gradient(to right, #243B55, #141E30); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */
  }
</style>