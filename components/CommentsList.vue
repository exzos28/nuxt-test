<template>
  <div class="scoped-wrap">
    <div v-if="loading">
      <a-skeleton
        class="skeleton"
        v-for="n in 3"
        active
        :key="n"
        :title="false"
        :paragraph="{ rows: 3 }"
      />
    </div>

    <a-list
      v-else
      class="comment-list"
      :header="`${comments.length} comments`"
      itemLayout="horizontal"
      :dataSource="comments"
    >
      <a-list-item slot="renderItem" slot-scope="item">
        <a-comment :author="item.name">
          <p slot="content">{{ item.body }}</p>
        </a-comment>
      </a-list-item>
    </a-list>
  </div>
</template>

<script>
export default {
  props: {
    comments: {
      type: Array,
      required: false
    },
    loading: {
      type: Boolean,
      required: false
    }
  }
};
</script>  

<style lang="scss" scoped>
.skeleton {
  margin-bottom: 30px;
}
.scoped-wrap {
  margin-top: 100px;
}
</style>