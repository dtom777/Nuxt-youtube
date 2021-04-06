<template>
  <v-container>
    <v-row class="grey lighten-4">
      <v-col cols="4" class="d-flex justify-center align-center">
        <nuxt-link to="/" class="headline black--text font-weight-bold"
          >NuxtTube</nuxt-link
        >
      </v-col>
      <v-col cols="6" offset="2">
        <v-form class="d-flex justify-center align-center">
          <v-text-field
            type="text"
            placeholder="キーワードを入力"
            v-model="query"
          />
          <v-btn :to="`/search/${this.query}`" class="blue ml-2">検索</v-btn>
        </v-form>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      query: "hikakin",
      apiKey: process.env.API_KEY
    };
  }
};
</script>
