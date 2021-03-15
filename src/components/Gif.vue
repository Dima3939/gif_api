<template>
  <div>
  <div class="gif" :style="`background-image: url(${gif.images.fixed_width.url})`">
  </div>
  <div class="share">
    <input ref="url" readonly type="text" :value="gif.images.original.url">
    <v-btn
        @click="copyUrl"
        block
        elevation="13"
        rounded
        large
    >
      <v-icon dark>
        Скопировать
      </v-icon>
    </v-btn>
  </div>
  </div>
</template>

<script>
export default {
  name: "Gif",
  props: {
    gif: Object
  },
  methods: {
    copyUrl() {
      this.$refs.url.select();
      document.execCommand('copy');
      this.$refs.url.value = 'Скопировано!';
    }
  },
}
</script>

<style scoped>
  .gif {
    width: 240px;
    height: 240px;
    background-repeat: no-repeat;
    background-size: cover;
    background-position: center;
    display: inline-flex;
    justify-content: center;
    align-items: flex-end;
  }
  .share {
    margin-bottom: 20px;
  }
  .share input {
    padding: 2px;
    color: white;
  }
  .v-btn ,input {
    margin-top: 10px;
  }
</style>