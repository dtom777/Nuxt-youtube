<template>
  <v-container fluid>
    <v-row>
      <v-col v-if="res" cols="12">
        <VideoPlay :videoId="id" />
        <p>{{ res.items[0].snippet.title }}</p>
        <div class="video-item">
          <pre>{{ res.items[0].snippet.description }}</pre>
        </div>
      </v-col>
      <!-- <div v-for="r in related" :key="r.id.videoId">
        <div>
          <nuxt-link :to="'/watch/' + r.id.videoId" v-if="r.snippet">
            <img
              v-if="r.snippet.thumbnails.medium.url"
              :src="r.snippet.thumbnails.medium.url"
              :alt="r.snippet.title"
            />
            <div class="info">
              <span>{{ r.snippet.title }}</span>
            </div>
          </nuxt-link>
        </div>
      </div> -->
    </v-row>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      id: this.$route.params.id
    };
  },
  async asyncData({ $axios, $config, params }) {
    const res = await $axios.$get(
      `${$config.apiUrl}/videos?type=video&part=snippet&regionCode=JP&id=${params.id}&key=${$config.apiKey}`
    );
    const related = await $axios.$get(
      `${$config.apiUrl}/search?type=video&part=snippet&maxResults=8&relatedToVideoId=${params.id}&key=${$config.apiKey}`
    );
    return {
      res,
      related: related.items
    };
  }
};
</script>
