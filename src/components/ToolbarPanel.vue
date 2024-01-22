<template>
  <div class="toolbar">
    <input class="toolbar-input" type="text" placeholder="Введите имя автора" />
    <button class="toolbar-button">Искать</button>
  </div>
</template>

<script>
export default {
  name: 'ToolbarPanel'
}
</script>

<style scoped>
.toolbar{
  display: flex;
  flex-direction: row;
  gap: 10px;
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
  padding: 0 24px;
  font-size: 14px;
  font-weight: 600;
  border-radius: 10px;
  border: none;
  cursor: pointer;
}

.toolbar-button:hover {
  background: #d3d3d3;
}
</style>
