<template>
  <div id="app">
    
      <div v-for="item in res.items" :key="item.id">
        <h1>{{item.snippet.title }}</h1>
        <img :src="item.snippet.thumbnails.standard.url" />
      </div>
    
  </div>
</template>

<script>
export default {
  name: 'app',
  data: function() {
    return {
      res: ''
    }
  },
  created() {
    this.getItems();
  },
  methods: {
    async getItems() {
      const response = await fetch(`https://www.googleapis.com/youtube/v3/playlists?part=snippet%2CcontentDetails&channelId=${process.env.VUE_APP_USER_ID}&maxResults=5&key=${process.env.VUE_APP_API_KEY}`);
      const items = await response.json();
      this.res = items;
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /* text-align: center; */
  color: #2c3e50;
  /* margin-top: 60px; */
}
</style>
