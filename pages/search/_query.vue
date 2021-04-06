<template>
  <v-container fluid>
    <v-row>
      <v-cos
        cols="12"
        v-for="r in res.items"
        :key="r.id.videoId"
        class="container"
      >
        <v-card
          nuxt
          tile
          :to="'/watch/' + r.id.videoId + '/'"
          v-if="r.snippet.thumbnails.medium.url"
        >
          <v-img
            :src="r.snippet.thumbnails.medium.url"
            :alt="r.snippet.title"
          />
          <v-card-title>{{ r.snippet.title }}</v-card-title>
          <v-card-subtitle>{{ r.snippet.channelTitle }}</v-card-subtitle>
        </v-card>
      </v-cos>
    </v-row>
  </v-container>
</template>

<script>
export default {
  async asyncData({ $axios, $config, params }) {
    const res = await $axios.$get(
      `${$config.apiUrl}/search?type=video&part=snippet&regionCode=JP&maxResults=10&q==${params.query}&key=${$config.apiKey}`
    );
    console.log(res.items);
    return { res };
  }
};
</script>
