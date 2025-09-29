<script setup lang="ts">
import { ref, onMounted, onBeforeUnmount } from 'vue';
import { ElImage } from 'element-plus';

const parallaxRef = ref<HTMLElement | null>(null);
const props = defineProps({
  src: {type: String},
  alt: {type: String},
  maxRotate: {type: Number, default: 0},
});

function handleParallaxMouseMove(e: MouseEvent) {
  console.log(props);
  const el = parallaxRef.value;
  if (!el) {return};
  const rect = el.getBoundingClientRect();
  const centerX = rect.width / 2;
  const centerY = rect.height / 2;
  const offsetX = e.clientX - rect.left;
  const offsetY = e.clientY - rect.top;
  const rotateX = (props['maxRotate'] * (offsetY - centerY)) / centerY * -1;
  const rotateY = (props['maxRotate'] * (offsetX - centerX)) / centerX;
  el.style.setProperty('--rotateX', rotateX.toString());
  el.style.setProperty('--rotateY', rotateY.toString());
}

function handleParallaxMouseLeave() {
  const el = parallaxRef.value;
  if (!el) return;
  el.style.setProperty('--rotateX', '0');
  el.style.setProperty('--rotateY', '0');
}

onMounted(() => {
  handleParallaxMouseLeave()
})
onBeforeUnmount(() => {
  handleParallaxMouseLeave()
})
</script>

<template>
    <div
      class="image-parallax"
      ref="parallaxRef"
      @mousemove="handleParallaxMouseMove"
      @mouseleave="handleParallaxMouseLeave"
    >
      <el-image :src="props.src" class="image" :alt="props.alt" />
    </div>
</template>

<style>

.image-parallax {
  perspective: 1200px;
  align-items: center;
  justify-content: center;
  aspect-ratio: 631/383;
  --rorateX: 0;
  --rotateY: 0;
}

.image {
  border-radius: 10px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s cubic-bezier(.25,.8,.25,1), box-shadow 0.2s;
  will-change: transform;
  width: 100%;
  height: 100%;
  /** 3D 旋转 */
  transform: rotateX(calc(var(--rotateX, 0) * 1deg)) rotateY(calc(var(--rotateY, 0) * 1deg));
}

</style>