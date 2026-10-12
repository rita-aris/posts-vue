<template>
  <form @submit.prevent>
    <h2>Создание поста</h2>
    <MyInput placeholder="Название" v-model="post.title" v-focus />
    <MyInput placeholder="Описание" v-model="post.body" />
    <MyButton customClass="btn_end" @click="createPost" :disabled="!isFormValid">Создать</MyButton>
  </form>
</template>

<script>
export default {
  data() {
    return {
      post: {
        title: '',
        body: ''
      }
    }
  },
  methods: {
    createPost() {
      this.post.id = Date.now();
      this.$emit('create', this.post);
      this.post = {
        title: '',
        body: ''
      }
    },
  },
  computed: {
    isFormValid() {
      return this.post.title.trim() !== '' && this.post.body.trim() !== '';
    }
  },
}
</script>

<style scoped>
form {
  display: flex;
  flex-direction: column;
}
</style>