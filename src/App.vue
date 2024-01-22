<template>
  <div class="posts-wrapper">
    <ToolbarPanel />
    <PostVue />
  </div>
</template>

<script>
import PostVue from './components/PostVue.vue'
import ToolbarPanel from './components/ToolbarPanel.vue'

export default {
  name: 'App',
  components: {
    PostVue,
    ToolbarPanel
  }
}
</script>

<style>
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: 60px 30px;
}

.posts-wrapper{
  display: flex;
  flex-direction: column;
  gap: 15px;
}
</style>
