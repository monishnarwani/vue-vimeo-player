<template>
  <div id="app">
    <vimeo-player :source="source" :identifier="identifier2" @onplay="videoPlayed" @onended="videoEnded" @onpause="videoPaused"></vimeo-player>
    <vimeo-player :source="source2" :identifier="identifier1" @onplay="videoPlayed1" :currentTime="10" @onended="videoEnded1" @onpause="videoPaused1"></vimeo-player>
  </div>
</template>

<script>
import VimeoPlayer from './components/VimeoPlayer'
export default {
  name: 'app',
  components: {
    VimeoPlayer
  },
  data() {
    return {
      source: 'https://vimeo.com/222665741',
      source2: 'https://vimeo.com/222785177',
      identifier1: 'video1',
      identifier2: 'video2'
    }
  },
  methods: {
    videoPlayed(event) {
      console.log('videoPlayed')
    },
    videoPlayed1(event) {
      console.log('videoPlayed1')
    },
    videoEnded(event) {
      console.log('videoEnded')
    },
    videoEnded1(event) {
      console.log('videoEnded1')
    },
    videoPaused(event) {
      console.log('videoPaused')
    },
    videoPaused1(event) {
      console.log('videoPaused1')
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
