<template>
  <div>
    <youtube :videoId="videoId" ref="youtube" :player-vars="{ autoplay: 1 }" />
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

<style></style>
