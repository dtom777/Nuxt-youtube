<template>
  <div>
    <div v-for="r in res.items" :key="r.id" class="container">
      <nuxt-link
        :to="'/watch/' + r.id"
        　class="item"
        v-if="r.snippet.thumbnails.standard"
      >
        <div class="video">
          <img
            :src="r.snippet.thumbnails.standard.url"
            :alt="r.snippet.title"
          />
          <span>{{ r.snippet.title }}</span>
        </div>
      </nuxt-link>
    </div>
  </div>
</template>

<script>
export default {
  async asyncData({ $axios, $config }) {
    const res = await $axios.$get(
      `${$config.apiUrl}/videos?type=video&part=snippet&maxResults=20&regionCode=JP&chart=mostPopular&key=${$config.apiKey}`
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
  justify-content: center;
  align-items: center;
  .item {
    display: flex;
    width: 50%;
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
