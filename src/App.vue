<template>
  <div id="app">
    <div class="toolbar">
      <label for="toolbar" class="toolbar-label">Фильтр по автору:</label>
      <input v-model="authorFilter" id="authorFilter" class="toolbar-input" placeholder="Введите имя автора" type="text"/>
      <button @click="filterPosts" class="toolbar-button">Искать</button>
    </div>
    <div v-if="loading">Загрузка...</div>
    <div v-else>
      <div v-for="post in filteredPosts" :key="post.id" class="post-content">
        <h2 class="post-title">{{ post.title }}</h2>
        <p class="post-description">{{ post.body }}</p>
        <p >Автор: {{ post.userId }}</p>
        <button @click="deletePost(post.id)" class="toolbar-button">Удалить</button>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

const api = axios.create({
  baseURL: 'https://jsonplaceholder.typicode.com'
})

export default {
  data () {
    return {
      posts: [],
      authorFilter: '',
      loading: true
    }
  },
  computed: {
    filteredPosts () {
      return this.posts.filter((post) => {
        return (
          this.authorFilter === '' ||
          post.userId.toString() === this.authorFilter
        )
      })
    }
  },
  methods: {
    filterPosts () {
      this.loading = true
      this.fetchPosts()
    },
    deletePost (postId) {
      api
        .delete(`/posts/${postId}`)
        .then(() => {
          this.posts = this.posts.filter((post) => post.id !== postId)
        })
        .catch((error) => {
          console.error('Ошибка при удалении поста:', error)
        })
    },
    fetchPosts () {
      api
        .get('/posts')
        .then((response) => {
          this.posts = response.data
        })
        .catch((error) => {
          console.error('Ошибка при загрузке постов', error)
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
#app{
  margin: 30px 20px;
}

.toolbar{
  display: flex;
  flex-direction: row;
  gap: 10px;
  align-items: center;
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
</style>
