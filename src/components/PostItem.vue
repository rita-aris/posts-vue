<template>
  <div class="post">
    <div>
      <div><strong><span v-html="highlightText(post.title, searchQuery)"></span></strong></div>
      <div>{{ post.body }}</div>
    </div>
    <div class="post__btns">
      <MyButton @click="$router.push(`/posts/${post.id}`)">Открыть</MyButton>
      <MyButton @click="$emit('remove', post)">Удалить</MyButton>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    post: {
      type: Object,
      required: true
    },
    searchQuery: {
      type: String,
      default: ''
    }
  },
  methods: {
    highlightText(text, query) {
      if (!query) return text;
      const regex = new RegExp(`(${query})`, 'gi');
      return text.replace(regex, '<span class="highlight">$1</span>');
    }
  }
}
</script>

<style scoped>
.post {
  display: flex;
  flex-direction: column;
  box-shadow: 0 0 10px 0 #8cacee;
  gap: 10px;
  padding: 10px;
  margin-top: 15px;
}
.post__btns {
  display: flex;
  align-items: center;
  gap: 10px;
}
</style>