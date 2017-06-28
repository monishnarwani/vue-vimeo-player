<template>
  <div>
    <div :id="options.identifier" :data-vimeo-url="options.source"></div>
  </div>
</template>

<script>
import Player from '@vimeo/player'
export default {
  props: {
    options: {
      type: Object,
      required: true
    }
  },
  data() {
    return {
      videoPlayer: null
    }
  },
  mounted() {
    this.videoPlayer = new Player(this.options.identifier)
    this.videoPlayer.on('play', (event) => {
      this.$emit('onplay', event)
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
