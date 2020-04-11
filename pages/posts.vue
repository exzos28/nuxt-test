<template>
  <div class="container list">
    <PostCard
      class="list__card"
      v-for="p in posts"
      :key="p.id"
      :id="p.id"
      :title="p.title"
      :body="p.body"
    />
  </div>
</template>
 
<script>
import axios from "axios";
import PostCard from "~/components/PostCard";
export default {
  middleware: "auth",
  async asyncData() {
    try {
      const response = await axios.get(
        "https://jsonplaceholder.typicode.com/posts"
      );
      const { data } = response;
      return {
        posts: data
      };
    } catch (e) {
      console.log(e);
    }
  },
  components: { PostCard },
  data() {
    return {
      posts: []
    };
  }
};
</script>

<style lang="scss">
.list {
  &__card {
    display: block;
    margin-bottom: 30px;
  }
}
</style>