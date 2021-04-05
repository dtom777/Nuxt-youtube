<template>
  <div class="container">
    <div v-if="res" class="video">
      <VideoPlay :videoId="id" class="video-item" />
      <p>{{ res.items[0].snippet.title }}</p>
      <hr />
      <div class="video-item">
        <pre>{{ res.items[0].snippet.description }}</pre>
      </div>
      <hr />
      <p>関連動画</p>
    </div>
    <div v-for="r in related" :key="r.id.videoId" class="sidenav">
      <div>
        <nuxt-link :to="'/watch/' + r.id.videoId" v-if="r.snippet" class="item">
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
    </div>
  </div>
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

<style lang="scss" scoped>
.container {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  flex-basis: 100%;
  width: 80%;
  justify-content: center;
  align-items: center;
  overflow-wrap: break-word;
  @media screen and (max-width: 560px) {
    width: 50%;
  }
  .video {
    width: 80%;
    .video-item {
      overflow-wrap: break-word;
    }
  }
  .sidenav {
    width: 480px;
    flex-basis: 480px;
    padding: 1rem;
    @media screen and (max-width: 960px) {
      width: 90%;
      margin: 1rem auto;
    }
    .item {
      display: flex;
      text-decoration: none;
      width: 100%;
      margin-bottom: 1rem;

      img {
        width: 50%;
        @media screen and (max-width: 560px) {
          width: 50%;
        }
      }
      .info {
        display: inline-block;
        width: 46%;
        padding: 2%;
        vertical-align: top;
        @media screen and (max-width: 560px) {
          width: 100%;
          padding: 0;
        }
      }
      span {
        color: white;
      }
    }
  }
}
</style>
