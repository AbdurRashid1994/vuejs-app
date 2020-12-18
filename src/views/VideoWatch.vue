<template>
  <div>
    <videoPlayer class="video-player-box" ref="videoPlayer" :options="playerOptions"></videoPlayer>
    <!-- <img :src="video.thumbnail" alt /> -->
    <h1>{{ video.name}}</h1>
    <div v-html="video.description"></div>
  </div>
</template>

<script>
import "video.js/dist/video-js.css";
import { videoPlayer } from "vue-video-player";

export default {
  components: {
    videoPlayer,
  },
  computed: {
    video() {
      return this.$store.state.videos.find(
        (vid) => vid.id == this.$route.params.id
      );
    },
    playerOptions() {
      return {
        language: "en",
        playbackRates: [0.5, 1.0, 1.5, 2.0, 2.5, 3.0],
        sources: [
          {
            muted: true,
            type: "video/mp4",
            src: this.video.videoUrl,
          },
        ],
        poster: this.video.thumbnail,
      };
    },
  },
};
</script>

<style>
.video-player-box .video-js {
  margin: auto;
}
/* img {
  max-width: 50%;
} */
</style>