<template>
  <div id="app">
    <h1>Посты</h1>
    <div>
      <label for="authorFilter">Фильтр по автору:</label>
      <input v-model="authorFilter" id="authorFilter" />
      <button @click="filterPosts">Применить фильтр</button>
    </div>
    <div v-if="loading">Загрузка...</div>
    <div v-else>
      <div v-for="post in filteredPosts" :key="post.id" class="post-card">
        <h2>{{ post.title }}</h2>
        <p>{{ post.body }}</p>
        <p>Автор: {{ post.userId }}</p>
        <button @click="deletePost(post.id)">Удалить</button>
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
.post-card {
  border: 1px solid #ccc;
  padding: 10px;
  margin: 10px 0;
}
</style>
