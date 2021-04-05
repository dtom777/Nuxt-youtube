<template>
  <div>
    <div v-for="r in res.items" :key="r.id.videoId" class="container">
      <nuxt-link
        :to="'/watch/' + r.id.videoId"
        class="item"
        v-if="r.snippet.thumbnails.medium.url"
      >
        <img :src="r.snippet.thumbnails.medium.url" :alt="r.snippet.title" />
        <span>{{ r.snippet.title }}</span>
      </nuxt-link>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      query: this.$route.params.query
    };
  },
  async asyncData({ $axios, $config, params }) {
    const res = await $axios.$get(
      `${$config.apiUrl}/search?type=video&part=snippet&regionCode=JP&maxResults=10&q==${params.query}&key=${$config.apiKey}`
    );
    console.log(res.items);
    return { res };
  }
};
</script>

<style lang="scss" scoped>
.container {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  flex-basis: 100%;
  justify-content: center;
  align-items: center;
  .item {
    display: block;
    width: 22.5%;
    margin: 1rem 1.25%;
    text-decoration: none;
    justify-content: center;
    align-items: center;
    @media screen and (max-width: 960px) {
      width: 70%;
      margin: 1rem 2.5%;
    }
    @media screen and (max-width: 560px) {
      width: 80%;
      margin: 1rem;
    }
    img {
      width: 100%;
    }
    span {
      color: white;
    }
  }
}
</style>
