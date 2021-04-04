<template>
  <div>
    <div v-for="r in res.items" :key="r.id" class="container">
      <div v-if="r.snippet.thumbnails.standard">
        <nuxt-link :to="'/watch/' + r.id" 　class="item">
          <img
            :src="r.snippet.thumbnails.standard.url"
            :alt="r.snippet.title"
          />
          <span>{{ r.snippet.title }}</span>
        </nuxt-link>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  async asyncData({ $axios, $config }) {
    const res = await $axios.$get(
      `${$config.apiUrl}/videos?type=video&part=snippet&maxResults=40&regionCode=JP&chart=mostPopular&key=${$config.apiKey}`
    );
    // console.log(res.items[0].snippet.thumbnails);
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
  .item {
    display: block;
    width: 22.5%;
    margin: 1rem 1.25%;
    text-decoration: none;
    @media screen and (max-width: 960px) {
      width: 45%;
      margin: 1rem 2.5%;
    }
    @media screen and (max-width: 560px) {
      width: 100%;
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
