<script setup>
import { ref, onMounted } from 'vue'

const roses = ref([])
const roseCount = 20

const emojis = ['🌹', '❤️', '💖', '💘', '💝'] // Mix of roses and hearts

const createRose = () => {
  return {
    id: Math.random(),
    left: Math.random() * 100 + 'vw',
    animationDuration: Math.random() * 3 + 2 + 's', // 2-5s
    animationDelay: Math.random() * 5 + 's',
    fontSize: Math.random() * 1.5 + 1 + 'rem', // 1-2.5rem
    emoji: emojis[Math.floor(Math.random() * emojis.length)]
  }
}

onMounted(() => {
  for (let i = 0; i < roseCount; i++) {
    roses.value.push(createRose())
  }
})
</script>

<template>
  <div class="roses-container">
    <div
      v-for="rose in roses"
      :key="rose.id"
      class="rose"
      :style="{
        left: rose.left,
        animationDuration: rose.animationDuration,
        animationDelay: rose.animationDelay,
        fontSize: rose.fontSize
      }"
    >
      {{ rose.emoji }}
    </div>
  </div>
</template>

<style scoped>
.roses-container {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  pointer-events: none; /* Make sure clicks pass through */
  z-index: 0; /* Behind everything */
  overflow: hidden;
}

.rose {
  position: absolute;
  top: -10%;
  animation-name: fall;
  animation-timing-function: linear;
  animation-iteration-count: infinite;
}

@keyframes fall {
  0% {
    transform: translateY(0) rotate(0deg);
    opacity: 1;
  }
  100% {
    transform: translateY(110vh) rotate(360deg);
    opacity: 0;
  }
}
</style>
