<template>
  <v-container fluid>
    <v-row>
      <v-col cols="6" sm="4" v-for="r in res.items" :key="r.id">
        <v-card
          nuxt
          tile
          :to="'/watch/' + r.id + '/'"
          v-if="r.snippet.thumbnails.standard"
        >
          <v-img
            :src="r.snippet.thumbnails.standard.url"
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
  async asyncData({ $axios, $config }) {
    const res = await $axios.$get(
      `${$config.apiUrl}/videos?type=video&part=snippet&maxResults=20&regionCode=JP&chart=mostPopular&key=${$config.apiKey}`
    );
    return { res };
  }
};
</script>

<style></style>
