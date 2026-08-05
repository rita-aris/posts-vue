<template>
  <div class="app">
    <MyModal v-model:show="isModalVisible">
      <PostForm @create="createPost" />
    </MyModal>
    <PostsList :posts="posts" @remove="removePost" v-if="!isPostsLoading" />
    <MyLoader v-else></MyLoader>
    <MyButton @click="showModal">Создать пост</MyButton>
  </div>
</template>

<script>
import PostForm from "@/components/PostForm.vue";
import PostsList from "@/components/PostsList.vue";
import MyModal from "@/components/UI/MyModal.vue";
import MyLoader from "@/components/UI/MyLoader.vue";
export default {
  components: {
    MyLoader,
    MyModal,
    PostForm, PostsList
  },
  data() {
    return {
      posts: [],
      isModalVisible: false,
      isPostsLoading: false,
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
    },
    async fetchPosts() {
      try {
        this.isPostsLoading = true;
        const response = await fetch('https://jsonplaceholder.typicode.com/posts?_limit=10');
        this.posts = await response.json();
      } catch (e) {
        console.error(e);
      } finally {
        this.isPostsLoading = false;
      }
    }
  },
  mounted() {
    this.fetchPosts();
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
  min-height: 100vh;
  height: 100%;
  padding: 20px;
  margin: 0 auto;
}
</style>