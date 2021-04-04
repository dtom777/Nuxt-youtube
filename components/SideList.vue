<template>
  <div>
    <div class="sidenav">Hello</div>
  </div>
</template>

<script>
export default {
  async asyncData({ $axios, $config, params }) {
    const res = await $axios.$get(
      `${$config.apiUrl}/search?type=video&part=snippet&relatedToVideoId=${params.id}&key=${$config.apiKey}`
    );
    console.log(1);
    return { res };
  }
};
</script>

<style lang="scss">
.sidenav {
}
</style>
