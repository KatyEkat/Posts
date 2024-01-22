<template>
  <div class="post">
    <div class="post-content">
      <h1 class="post-title">title</h1>
      <p class="post-description">description</p>
    </div>
    <CloseIcon />
  </div>
</template>

<script>
import CloseIcon from './CloseIcon.vue'

export default {
  name: 'PostVue',
  // props: {
  //   msg: String
  // },
  components: { CloseIcon }
}

</script>

<style scoped>
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
  gap: 10px;
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
