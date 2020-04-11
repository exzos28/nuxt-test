<template>
  <div class="container scoped-wrap">
    <a-skeleton active :paragraph="{ rows: 14 }" v-if="loading" />
    <p v-else-if="error">
      Ошибка. Мы не знаем что это такое
      <br />
      {{error}}
    </p>
    <div v-else>
      <h1 class="title">{{post.title}}</h1>
      <p>{{post.body}}</p>
    </div>

    <CommentsList :loading="loading" :comments="comments" />
  </div>
</template>
<script>
import axios from "axios";
import CommentsList from "~/components/CommentsList";
export default {
  middleware: "auth",
  data() {
    return {
      post: [],
      comments: [],
      loading: true,
      error: null
    };
  },
  components: { CommentsList },
  methods: {
    handleClick() {
      this.loading = !this.loading;
    }
  },
  async mounted() {
    try {
      const { id } = this.$route.params;
      const postResponse = await axios.get(
        `https://jsonplaceholder.typicode.com/posts/${id}`
      );
      const commentsResponse = await axios.get(
        `https://jsonplaceholder.typicode.com/posts/${id}/comments`
      );

      const { data: post } = postResponse;
      const { data: comments } = commentsResponse;
      
      this.post = post;
      this.loading = false;
      this.comments = comments;
    } catch (e) {
      this.error = e;
      this.loading = false;
    }
  }
};
</script>

<style lang="scss" scoped>
.scoped-wrap {
  padding-top: 50px;
}
</style>