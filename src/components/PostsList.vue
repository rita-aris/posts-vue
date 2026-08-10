<template>
  <div class="posts-list">
    <div v-if="posts.length > 0">
      <h1>Список постов</h1>
      <TransitionGroup name="list">
        <PostItem v-for="post in posts" :post="post" :key="post.id" @remove="$emit('remove', post)" />
      </TransitionGroup>
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
  position: relative;
  margin-top: 30px;
}
.list-move,
.list-enter-active,
.list-leave-active {
  transition: all 0.5s ease;
}
.list-enter-from,
.list-leave-to {
  opacity: 0;
  transform: translateX(20px);
}
.list-leave-active {
  position: absolute;
}
</style>