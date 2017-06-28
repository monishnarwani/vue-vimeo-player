<template>
  <div>
    <div :id="identifier" :data-vimeo-url="source"></div>
  </div>
</template>

<script>
import Player from '@vimeo/player'
export default {
  props: {
    source: {
      type: String,
      required: true
    },
    identifier: {
      type: String,
      required: true
    },
    currentTime: {
      type: Number,
      default: 0
    }
  },
  data() {
    return {
      videoPlayer: null
    }
  },
  mounted() {
    this.videoPlayer = new Player(this.identifier)
    if(this.currentTime > 0) {
      this.videoPlayer.setCurrentTime(this.currentTime)
    }
    this.videoPlayer.on('play', (event) => {
      this.$emit('onplay', event)
      // if(this.currentTime == event.seconds) { //if we want to stop autoplay
      //   this.videoPlayer.pause()
      // }
    })
    this.videoPlayer.on('pause', (event) => {
      this.$emit('onpause', event)
    })
    this.videoPlayer.on('ended', (event) => {
      this.$emit('onended', event)
    })
    this.videoPlayer.on('error', (event) => {
      this.$emit('onerror', event)
    })

  },
  beforeDestroy() {
    this.videoPlayer.off('play')
    this.videoPlayer.off('pause')
    this.videoPlayer.off('ended')
    this.videoPlayer.off('error')
  }
}
</script>
