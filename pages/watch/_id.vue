<template>
  <v-container fluid>
    <v-row>
      <v-col v-if="res" cols="8">
        <VideoPlay :videoId="id" />
        <h2>{{ res.items[0].snippet.title }}</h2>
        <pre>{{ res.items[0].snippet.description }}</pre>
      </v-col>
      <v-col cols="4">
        <div v-for="r in related" :key="r.id.videoId">
          <v-card>
            <nuxt-link :to="'/watch/' + r.id.videoId" v-if="r.snippet">
              <v-img
                v-if="r.snippet.thumbnails.medium.url"
                :src="r.snippet.thumbnails.medium.url"
                :alt="r.snippet.title"
              />
              <v-card-title class="subtitle-1 black--text">{{
                r.snippet.title
              }}</v-card-title>
            </nuxt-link>
          </v-card>
        </div>
      </v-col>
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

<style>
pre {
  white-space: pre-wrap;
}
</style>
