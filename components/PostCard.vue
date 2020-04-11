<template>
  <nuxt-link :to="link">
    <div class="card">
      <div class="card-content">
        <div class="media">
          <div class="media-content">
            <p class="title is-4">{{title}}</p>
          </div>
        </div>

        <div class="content">{{body}}</div>
      </div>
    </div>
  </nuxt-link>
</template>
<script>
export default {
  data() {
    return {
      loading: false
    };
  },
  props: {
    title: { type: String, required: true },
    body: { type: String, required: true },
    id: {
      type: Number,
      required: true
    }
  },
  computed: {
    link() {
      return this.id.toString();
    }
  },
  methods: {}
};
</script>
<style lang="scss" scoped>
.text {
  text-decoration: none;
  color: #000;
}
</style>