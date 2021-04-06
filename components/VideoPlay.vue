<template>
  <div class="wrap">
    <youtube
      :videoId="videoId"
      ref="youtube"
      :player-vars="{ autoplay: 1 }"
      class="video"
    />
  </div>
</template>

<script>
import "../plugins/vue-youtube";
export default {
  props: {
    videoId: {
      type: String,
      default: ""
    }
  },
  computed: {
    player() {
      return this.$refs.youtube.player;
    }
  }
};
</script>

<style lang="scss">
.wrap {
  position: relative;
  width: 100%;
  &:before {
    display: block;
    content: "";
    padding-top: 56.2%;
  }
  .video {
    position: absolute;
    top: 0;
    left: 0;
    width: 100% !important;
    height: 100% !important;
  }
}
</style>
