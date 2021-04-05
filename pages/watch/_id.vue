<template>
  <div>
    {{ id }}
    <div v-if="res">
      <VideoPlay :videoId="id" />
      <p>{{ res.items[0].snippet.title }}</p>
      <hr />
      <div>
        <pre>{{ res.items[0].snippet.description }}</pre>
      </div>
    </div>
    <!-- <div v-for="r in related" :key="r.snippet">{{ r }}</div> -->
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
    return { res };
  }
  // async asyncData({ $axios, $config, params }) {
  //   const res = await $axios.$get(
  //     `${$config.apiUrl}/videos?type=video&part=snippet&regionCode=JP&id=${params.id}&key=${$config.apiKey}`
  //   );
  //   const related = await $axios.$get(
  //     `${$config.apiUrl}/search?type=video&part=snippet&maxResults=7&relatedToVideoId=${params.id}&key=${$config.apiKey}`
  //   );
  //   console.log(related.items);
  //   return {
  //     res,
  //     related: related.items
  //   };
  // }
};
</script>

<style></style>
