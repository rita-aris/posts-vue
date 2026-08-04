<template>
  <div class="app">
    <MyModal v-model:show="isModalVisible">
      <PostForm @create="createPost" />
    </MyModal>
    <PostsList :posts="posts" @remove="removePost" />
    <MyButton @click="showModal">Создать пост</MyButton>
  </div>
</template>

<script>
import PostForm from "@/components/PostForm.vue";
import PostsList from "@/components/PostsList.vue";
import MyModal from "@/components/UI/MyModal.vue";
export default {
  components: {
    MyModal,
    PostForm, PostsList
  },
  data() {
    return {
      posts: [
        {id: 1, title: 'JavaScript', body: 'Погружение в Асинхронное Программирование'},
        {id: 2, title: 'Современные Тенденции', body: 'ES2022 и Что Нового в JavaScript'},
        {id: 3, title: 'От Функций до Объектов', body: 'Понимание Основ JavaScript'},
      ],
      isModalVisible: false,
    }
  },
  methods: {
    createPost(post) {
      this.posts.push(post);
      this.isModalVisible = false;
    },
    removePost(post) {
      this.posts = this.posts.filter(p => p.id !== post.id);
    },
    showModal() {
      this.isModalVisible = true;
    }
  }
}
</script>

<style>
* {
  font-family: "Inter", sans-serif;
  box-sizing: border-box;
  color: #3B4256;
  padding: 0;
  margin: 0;
}
body {
  background-color: #E7F2FD;
}
.app {
  background-color: #fff;
  max-width: 1000px;
  height: 100vh;
  padding: 20px;
  margin: 0 auto;
}

</style>