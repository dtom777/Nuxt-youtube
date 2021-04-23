<template>
  <v-container fluid>
    <v-row>
      <v-col
        cols="6"
        sm="4"
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
          <v-card-title class="d-block text-truncate">
            {{ r.snippet.title }}
          </v-card-title>
          <v-card-subtitle>{{ r.snippet.channelTitle }}</v-card-subtitle>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  async asyncData({ $axios, $config, params, error }) {
    try {
      const res = await $axios.$get(
        `${$config.apiUrl}/search?type=video&part=snippet&regionCode=JP&maxResults=12&q==${params.query}&key=${$config.apiKey}`
      );
      console.log(res.items);
      return { res };
    } catch (err) {
      error({
        statusCode: err.response.status,
        message: err.response.data.message
      });
    }
  }
};
</script>
