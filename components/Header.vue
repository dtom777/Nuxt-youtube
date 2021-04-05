<template>
  <div class="header">
    <div class="item">
      <nuxt-link to="/">NuxtTube</nuxt-link>
    </div>
    <div class="item">
      <form>
        <input type="text" placeholder="キーワードを入力" v-model="query" />
        <nuxt-link :to="`/search/${this.query}`">
          <button>検索</button>
        </nuxt-link>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      query: "hikakin",
      apiKey: process.env.API_KEY
    };
  },
  methods: {
    searchVideo() {
      this.$router.push("/");
      // this.$router.push({
      //   path: "search",
      //   query: {
      //     type: video,
      //     part: snippet,
      //     q: this.query,
      //     maxResults: 3,
      //     key: this.apiKey
      //   }
      // });
    }
  }
};
</script>

<style lang="scss" scoped>
.header {
  display: flex;
  height: 56px;
  width: 100%;
  background-color: #202020;
  a {
    color: white;
    font-size: 1.2rem;
    line-height: 1rem;
    padding-left: 1rem;
    text-decoration: none;
    font-weight: 600;
  }
  .item {
    &:first-child {
      flex-grow: 1;
      line-height: 56px;
    }
    &:last-child {
      flex-grow: 2;
    }
    form {
      width: 50%;
      height: 32px;
      display: flex;
      margin: 12px 0;
      @media screen and(max-width:960px) {
        width: 420px;
        margin: 1rem 2.5%;
      }
      @media screen and(max-width:560px) {
        width: 80%;
        margin: 1rem auto;
      }
      input {
        width: 80%;
        text-indent: 0.5rem;
        border: #121212;
        background-color: white;
      }
      button {
        width: 50px;
      }
    }
  }
}
</style>
