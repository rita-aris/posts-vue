<template>
  <div>
    <h1>Страница с постами</h1>
    <div class="top-bar">
      <MyInput customClass="input_search" placeholder="Поиск по названию..." v-model="searchQuery" v-focus />
      <MyButton @click="showModal">Создать пост</MyButton>
      <MySelect v-model="selectedSort" :options="sortOptions" v-if="sortedAndSearchedPosts.length > 0" />
    </div>
    <MyModal v-model:show="isModalVisible">
      <PostForm @create="createPost" />
    </MyModal>
    <PostsList :posts="sortedAndSearchedPosts" @remove="removePost" v-if="!isPostsLoading" :searchQuery="searchQuery" />
    <MyLoader v-else />
    <!--Если нужна постраничная пагинация, добавь компонент MyPagination, функции changePage, page -->
    <!--<MyPagination :totalPages="totalPages" :page="page" @change="changePage" />-->
    <div class="observer" v-intersection="loadMorePosts"></div>
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
      ],
      page: 1,
      limit: 10,
      totalPages: 0,
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
        const response = await fetch(`https://jsonplaceholder.typicode.com/posts?_limit=${this.limit}&_page=${this.page}`);
        this.totalPages = Math.ceil(response.headers.get('X-Total-Count') / this.limit);
        this.posts = await response.json();
      } catch (e) {
        console.error(e);
      } finally {
        this.isPostsLoading = false;
      }
    },
    async loadMorePosts() {
      try {
        this.page = this.page + 1;
        const response = await fetch(`https://jsonplaceholder.typicode.com/posts?_limit=${this.limit}&_page=${this.page}`);
        this.totalPages = Math.ceil(response.headers.get('X-Total-Count') / this.limit);
        const posts = await response.json();
        this.posts = [...this.posts, ...posts];
      } catch (e) {
        console.error(e);
      }
    },
    // changePage(pageNumber) {
    //   this.page = pageNumber;
    // }
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
  watch: {
    // page() {
    //   this.fetchPosts();
    // }
  }
}
</script>

<style scoped>
.top-bar {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 10px;
  flex-wrap: wrap;
}
.observer {
  height: 30px;
}
@media screen and (max-width: 480px) {
  .top-bar {
    flex-direction: column;
    align-items: flex-start;
  }
}
</style>