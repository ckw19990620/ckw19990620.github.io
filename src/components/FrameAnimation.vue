<template>
  <div class="frame-animation-container" ref="containerRef">
    <div class="animation-canvas" :style="canvasStyle">
  <img 
    v-for="(frame, index) in frames" 
    :key="index"
    :src="frame"
    :class="['frame', { active: currentFrameIndex === index }]"
    :style="{ top: `${index * props.frameHeight}px` }"
    alt="Animation frame"
  />
</div>
    <div class="progress-indicator">
      <div class="progress-bar" :style="{ width: progress + '%' }"></div>
    </div>
    <div class="controls">
      <span class="frame-counter">
        Frame: {{ currentFrameIndex + 1 }} / {{ totalFrames }}
      </span>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, computed, onMounted, onUnmounted } from 'vue'

const props = defineProps({
  frameCount: {
    type: Number,
    default: 60
  },
  frameHeight: {
    type: Number,
    default: 800
  },
  sensitivity: {
    type: Number,
    default: 1.0
  }
})

const containerRef = ref<HTMLElement | null>(null)
const currentFrameIndex = ref(0)
const totalFrames = props.frameCount

// 生成帧图片URL - 使用本地图片文件
const frames = computed(() => {
  return Array.from({ length: totalFrames }, (_, index) => {
    const frameNumber = (index % 10) + 1
    return `/images/frames/frame-${frameNumber}.jpg`
  })
})

const progress = computed(() => {
  return ((currentFrameIndex.value + 1) / totalFrames) * 100
})

const canvasStyle = computed(() => ({
  height: `${totalFrames * props.frameHeight}px`
}))

const handleScroll = (event: WheelEvent) => {
  if (!containerRef.value) return
  
  const delta = event.deltaY * props.sensitivity
  const scrollAmount = Math.abs(delta) / 100
  
  if (delta > 0) {
    // 向下滚动
    currentFrameIndex.value = Math.min(
      totalFrames - 1,
      currentFrameIndex.value + Math.ceil(scrollAmount)
    )
  } else {
    // 向上滚动
    currentFrameIndex.value = Math.max(
      0,
      currentFrameIndex.value - Math.ceil(scrollAmount)
    )
  }
}

const handleKeyPress = (event: KeyboardEvent) => {
  if (event.key === 'ArrowDown') {
    currentFrameIndex.value = Math.min(totalFrames - 1, currentFrameIndex.value + 1)
  } else if (event.key === 'ArrowUp') {
    currentFrameIndex.value = Math.max(0, currentFrameIndex.value - 1)
  }
}

onMounted(() => {
  if (containerRef.value) {
    containerRef.value.addEventListener('wheel', handleScroll, { passive: false })
    window.addEventListener('keydown', handleKeyPress)
  }
})

onUnmounted(() => {
  if (containerRef.value) {
    containerRef.value.removeEventListener('wheel', handleScroll)
    window.removeEventListener('keydown', handleKeyPress)
  }
})
</script>

<style scoped>
.frame-animation-container {
  position: relative;
  width: 100%;
  height: 100vh;
  overflow: hidden;
  background: #1a1a1a;
}

.animation-canvas {
  position: relative;
  width: 100%;
  transition: transform 0.1s ease-out;
  transform: translateY(calc(-1px * v-bind('currentFrameIndex * frameHeight')));
}

.frame {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: v-bind('frameHeight + "px"');
  object-fit: cover;
  opacity: 0;
  transition: opacity 0.3s ease;
}

.frame.active {
  opacity: 1;
}

.progress-indicator {
  position: fixed;
  top: 20px;
  left: 50%;
  transform: translateX(-50%);
  width: 300px;
  height: 4px;
  background: rgba(255, 255, 255, 0.3);
  border-radius: 2px;
  z-index: 100;
}

.progress-bar {
  height: 100%;
  background: linear-gradient(90deg, #ff6b6b, #4ecdc4);
  border-radius: 2px;
  transition: width 0.2s ease;
}

.controls {
  position: fixed;
  bottom: 20px;
  left: 50%;
  transform: translateX(-50%);
  color: white;
  font-family: 'Arial', sans-serif;
  font-size: 14px;
  background: rgba(0, 0, 0, 0.7);
  padding: 8px 16px;
  border-radius: 20px;
  z-index: 100;
}

.frame-counter {
  opacity: 0.8;
}

/* 响应式设计 */
@media (max-width: 768px) {
  .progress-indicator {
    width: 200px;
  }
  
  .controls {
    font-size: 12px;
  }
}
</style>