<template>
  <div class="home">
    <h1>Videos</h1>
    <div class="video-container">
      <div v-for="video in videos" :key="video.name">
        <router-link :to="{name: 'video-watch', params: {id: video.id}}">
          <div class="video-box">
            <img :src="video.thumbnail" alt />
            <div>
              <h3>{{ video.name }}</h3>
              <div v-html="video.description"></div>
            </div>
          </div>
        </router-link>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'
import Api from '@/services/api.js'

export default {
  name: "Home",
  components: {
    // HelloWorld
  },
  mounted() {
    Api().get('/videos').then((response)=>{
      this.videos=response.data;
    })
  },
  data() {
    return {
      // videos: this.$store.state.videos,
      videos: []
    };
  },
};
</script>

<style lang="scss" scoped>
.home {
  .video-container {
    .video-box {
      border: 1px solid black;
      border-radius: 10px;
      margin: 10px;
      padding: 10px;
      text-align: left;
      display: flex;
      justify-content: flex-start;
      img {
        width: 200px;
        padding: 10px;
      }
    }
  }
}
</style>