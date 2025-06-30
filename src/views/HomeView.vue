<script setup lang="ts">
import { ref, onMounted, onBeforeUnmount } from 'vue'
const button = {
  type: 'warning',
  color: '#fcd34d',
  round: true,
}

const parallaxRef = ref<HTMLElement | null>(null)
const maxRotate = 3

function handleParallaxMouseMove(e: MouseEvent) {
  const el = parallaxRef.value
  if (!el) return
  const rect = el.getBoundingClientRect()
  const centerX = rect.width / 2
  const centerY = rect.height / 2
  const offsetX = e.clientX - rect.left
  const offsetY = e.clientY - rect.top
  const rotateX = (maxRotate * (offsetY - centerY)) / centerY * -1
  const rotateY = (maxRotate * (offsetX - centerX)) / centerX
  el.style.setProperty('--rotateX', rotateX.toString())
  el.style.setProperty('--rotateY', rotateY.toString())
}
function handleParallaxMouseLeave() {
  const el = parallaxRef.value
  if (!el) return
  el.style.setProperty('--rotateX', '0')
  el.style.setProperty('--rotateY', '0')
}

onMounted(() => {
  handleParallaxMouseLeave()
})
onBeforeUnmount(() => {
  handleParallaxMouseLeave()
})
</script>

<template>
  <div class="home-container">
    <div
      class="poster-parallax"
      ref="parallaxRef"
      @mousemove="handleParallaxMouseMove"
      @mouseleave="handleParallaxMouseLeave"
      style="--rotateX:0;--rotateY:0;--maxRotate:15;"
    >
      <el-image src="/imgs/home/main.webp" class="poster" alt="乐队养的耄耋" />
    </div>
    <h1 class="title">欢迎来到 Crychic 乐队</h1>
    <el-button class="explore-button" :round="button.round" :color="button.color">咕咕嘎咕</el-button>
  </div>
</template>

<style>
.home-container {
  display: flex;
  width: 100%;
  max-width: 100%;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  text-align: center;
  background: linear-gradient(135deg, #ff9a9e, #fad0c4);
  min-height: 100vh;
  padding: 20px;
}

.poster-parallax {
  perspective: 1200px;
  display: flex;
  align-items: center;
  justify-content: center;
  aspect-ratio: 631/383;
  max-width: 80vw;
  max-height: 80vh;
  margin-bottom: 24px;
}

.poster {
  border-radius: 10px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s cubic-bezier(.25,.8,.25,1), box-shadow 0.2s;
  will-change: transform;
  width: 100%;
  height: 100%;
  /* 3D 旋转 */
  transform: rotateX(calc(var(--rotateX, 0) * 1deg)) rotateY(calc(var(--rotateY, 0) * 1deg));
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
