<script setup lang="ts">
const button = {
  type: 'primary',
  color: '#e65c50',
  round: true,
}
</script>

<template>
  <div class="home-container">
    <img src="/imgs/home/main.webp" class="poster" alt="要乐奈" />
    <h1 class="title">欢迎来到 MyGO FanSite</h1>
    <p class="description">探索 MyGO 和 Ave Mujica 的精彩剧情，感受音乐的魅力！</p>
    <el-button class="explore-button" :round="button.round" :color="button.color">了解更多</el-button>
  </div>
</template>

<style>
.home-container {
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  text-align: center;
  background: linear-gradient(135deg, #ff9a9e, #fad0c4);
  min-height: 100vh;
  padding: 20px;
}

.poster {
  width: 80%;
  border-radius: 10px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  animation: fadeIn 2s ease-in-out;
}

.title {
  font-size: 2.5rem;
  color: #333;
  margin: 20px 0 10px;
}

.description {
  font-size: 1.2rem;
  color: #555;
  margin-bottom: 20px;
}

.explore-button {
  cursor: pointer;
}

@keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}
</style>
