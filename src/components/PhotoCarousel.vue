<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const props = defineProps({
  images: {
    type: Array,
    required: true
  },
  quotes: {
    type: Array,
    required: true
  }
})

const currentIndex = ref(0)
let intervalId = null

const nextSlide = () => {
  currentIndex.value = (currentIndex.value + 1) % props.images.length
}

onMounted(() => {
  intervalId = setInterval(nextSlide, 3000)
})

onUnmounted(() => {
  if (intervalId) clearInterval(intervalId)
})
</script>

<template>
  <div class="carousel">
    <div v-for="(img, index) in images" :key="index" class="slide" :class="{ active: index === currentIndex }">
      <img :src="img" alt="Our Memory" />
      <p class="quote">{{ quotes[index] }}</p>
    </div>
  </div>
</template>

<style scoped>
.carousel {
  position: relative;
  width: 100%;
  max-width: 600px;
  height: 500px;
  overflow: hidden;
  border-radius: 20px;
  box-shadow: 0 10px 20px rgba(0,0,0,0.1);
  margin-bottom: 30px;
  background-color: white;
}

.slide {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  opacity: 0;
  transition: opacity 1s ease-in-out;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.slide.active {
  opacity: 1;
}

.slide img {
  width: 100%;
  height: 80%;
  object-fit: cover;
}

.quote {
  padding: 15px;
  font-style: italic;
  color: #880e4f;
  font-size: 1.1rem;
  margin: 0;
}
</style>
