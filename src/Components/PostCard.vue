<template>
  <div class="post">
    <div class="post-block">
      <h2 class="post-title">{{ post.title }}</h2>
      <p class="post-description">{{ post.body }}</p>
      <p>Автор: {{ post.userId }}</p>
    </div>
    <button @click="deletePost" class="toolbar-button">Удалить</button>
  </div>
</template>

<script>
export default {
  props: {
    post: {
      type: Object,
      required: true
    },
    onDelete: {
      type: Function,
      required: true
    }
  },
  methods: {
    deletePost () {
      this.onDelete(this.post.id)
    }
  }
}
</script>

<style scoped>
.post {
  display: flex;
}

.post-block {
  padding: 10px 25px;
  border-radius: 10px;
  width: 100%;
  height: auto;
  display: flex;
  justify-content: space-between;
  flex-direction: column;
}

.post-content {
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

.toolbar-button {
  width: 120px;
  height: 45px;
  font-size: 14px;
  font-weight: 600;
  border-radius: 10px;
  border: none;
  cursor: pointer;
}
</style>
