<template>
  <div class="post">
    <div>
      <div><strong><span v-html="highlightText(post.title, searchQuery)"></span></strong></div>
      <div>{{ post.body }}</div>
    </div>
    <div class="post__btns">
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
  align-items: center;
  justify-content: space-between;
  box-shadow: 0 0 10px 0 #8cacee;
  gap: 10px;
  padding: 10px;
  margin-top: 15px;
}
@media screen and (max-width: 480px) {
  .post {
    flex-direction: column;
    align-items: flex-start;
  }
}
</style>