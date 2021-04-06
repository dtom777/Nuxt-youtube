<template>
  <v-container>
    <v-row>
      <v-col cols="8">
        <youtube
          :videoId="videoId"
          ref="youtube"
          :player-vars="{ autoplay: 1 }"
        />
      </v-col>
    </v-row>
  </v-container>
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
