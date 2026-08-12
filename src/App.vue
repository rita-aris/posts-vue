<template>
  <div class="app">
    <h1>Страница с постами</h1>
    <div class="top-bar">
      <MyInput customClass="input_search" placeholder="Поиск по названию..." v-model="searchQuery" />
      <MyButton @click="showModal">Создать пост</MyButton>
      <MySelect v-model="selectedSort" :options="sortOptions" v-if="sortedAndSearchedPosts.length > 0" />
    </div>
    <MyModal v-model:show="isModalVisible">
      <PostForm @create="createPost" />
    </MyModal>
    <PostsList :posts="sortedAndSearchedPosts" @remove="removePost" v-if="!isPostsLoading" :searchQuery="searchQuery" />
    <MyLoader v-else />
  </div>
</template>

<script>
import PostForm from "@/components/PostForm.vue";
import PostsList from "@/components/PostsList.vue";
export default {
  components: {
    PostForm,
    PostsList
  },
  data() {
    return {
      posts: [],
      isModalVisible: false,
      isPostsLoading: false,
      searchQuery: '',
      selectedSort: '',
      sortOptions: [
        {value: 'title', name: 'По названию'},
        {value: 'body', name: 'По описанию'},
      ]
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
  },
  computed: {
    sortedPosts() {
      if (this.selectedSort) {
        return [...this.posts].sort((p1, p2) => p1[this.selectedSort].localeCompare(p2[this.selectedSort]));
      }
      return this.posts;
    },
    sortedAndSearchedPosts() {
      if (this.searchQuery) {
        return this.sortedPosts.filter(p => p.title.toLowerCase().includes(this.searchQuery.toLowerCase()));
      }
      return this.sortedPosts;
    }
  },
  watch: {}
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
.top-bar {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 10px;
  flex-wrap: wrap;
}
.highlight {
  background-color: #FFEA8A;
}
@media screen and (max-width: 480px) {
  .top-bar {
    flex-direction: column;
    align-items: flex-start;
  }
}
</style>