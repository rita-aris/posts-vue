<template>
  <div class="posts-list">
    <div v-if="posts.length > 0">
      <h1>Список постов</h1>
      <PostItem v-for="post in posts" :post="post" :key="post.id" @remove="$emit('remove', post)" />
    </div>
    <h3 v-else>Список постов пуст</h3>
  </div>
</template>

<script>
import PostItem from "@/components/PostItem.vue";
export default {
  components: {PostItem},
  props: {
    posts: {
      type: Array,
      required: true
    }
  }
}
</script>

<style scoped>
.posts-list {
  margin-top: 30px;
}
</style>