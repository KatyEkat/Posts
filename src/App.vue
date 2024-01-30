<template>
  <div id="app">
    <h1>Посты</h1>
    <div class='toolbar'>
      <label for="authorFilter" class="toolbar-label">Фильтр по автору:</label>
      <input v-model="authorFilter" id="authorFilter" placeholder='Введите имя автора' class="toolbar-input"/>
      <button @click="filterPosts" class="toolbar-button">Искать</button>
    </div>
    <div v-if="loading">Загрузка...</div>
    <div v-else>
      <PostCard
        class='post-card'
        v-for="post in filteredPosts"
        :key="post.id"
        :post="post"
        :on-delete="deletePost"
        style='margin-bottom: 10px;'
      ></PostCard>
    </div>
  </div>
</template>

<script>
import PostCard from './Components/PostCard.vue'
import { getPosts, deletePost } from './api/api'

export default {
  data () {
    return {
      posts: [],
      authorFilter: '',
      loading: true
    }
  },
  components: {
    PostCard
  },
  computed: {
    filteredPosts () {
      return this.posts.filter(post => {
        return this.authorFilter === '' || post.userId.toString() === this.authorFilter
      })
    }
  },
  methods: {
    filterPosts () {
      this.loading = true
      this.fetchPosts()
    },
    deletePost (postId) {
      deletePost(postId)
        .then(() => {
          this.posts = this.posts.filter(post => post.id !== postId)
        })
        .catch(error => {
          console.error('Ошибка при удалении поста:', error)
        })
    },
    fetchPosts () {
      getPosts()
        .then(response => {
          this.posts = response.data
        })
        .catch(error => {
          console.error('Ошибка при загрузке постов:', error)
        })
        .finally(() => {
          this.loading = false
        })
    }
  },
  mounted () {
    this.fetchPosts()
  }
}
</script>

<style>
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

#app{
  margin: 30px 20px;
}

.toolbar{
  display: flex;
  flex-direction: row;
  gap: 10px;
  align-items: center;
  margin-bottom: 15px;
}

.toolbar-label{
  font-size: 16px;
  font-style: normal;
  width: 200px;
}
.toolbar-input {
  width: 100%;
  height: 36px;
  border-radius: 10px;
  font-size: 16px;
  font-weight: normal;
  padding: 0 15px;
  border: 1px solid #f0f0f0;
}

.toolbar-button {
  padding: 10px 24px;
  font-size: 14px;
  font-weight: 600;
  border-radius: 10px;
  border: none;
  cursor: pointer;
}

.toolbar-button:hover {
  background: #d3d3d3;
}

.post {
  padding: 10px 25px;
  border-radius: 10px;
  border: 1px solid gray;
  width: 100%;
  height: auto;
  display: flex;
  justify-content: space-between;
}

.post-content{
  display: flex;
  flex-direction: column;
  align-items: flex-start;
}

.post-title {
  font-size: 26px;
  font-style: normal;
}

.post-description {
  font-size: 16px;
  font-style: normal;
}

.post-card{
  margin-bottom: 10px;
}
</style>
