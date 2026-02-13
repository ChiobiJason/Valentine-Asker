<script setup>
import { ref } from 'vue'
import PhotoCarousel from './PhotoCarousel.vue'

// Import images
import img1 from '../assests/images/Instagram Photo 497325065.jpg'
import img2 from '../assests/images/Instagram Photo 566026197.jpg'
import img3 from '../assests/images/Instagram Photo 566754140.jpg'
import img4 from '../assests/images/Instagram Photo 588375592.jpg'
import img5 from '../assests/images/Instagram Photo 588394134.jpg'
import img6 from '../assests/images/Instagram Photo 588645226.jpg'
import img7 from '../assests/images/Instagram Photo Download (1).jpg'
import img8 from '../assests/images/Instagram Photo Download.jpg'

const images = [img1, img2, img3, img4, img5, img6, img7, img8]
const quotes = [
  "You are my sun, my moon, and all my stars.",
  "I look at you and see the rest of my life in front of my eyes.",
  "Every love story is beautiful, but ours is my favorite.",
  "I love you more than words can wield the matter, Dearer than eye-sight, space, and liberty.",
  "If I know what love is, it is because of you.",
  "My heart is and always will be yours.",
  "You are the finest, loveliest, tenderest, and most beautiful person I have ever known.",
  "I swear I couldn't love you more than I do right now, and yet I know I will tomorrow."
]

const yesButtonSize = ref(1)
const showSuccess = ref(false)

const handleNoClick = () => {
  yesButtonSize.value += 0.5
}

import emailjs from '@emailjs/browser'

// ... imports ...

const handleYesClick = () => {
  showSuccess.value = true
  
  // EmailJS Configuration
  const SERVICE_ID = import.meta.env.APP_EMAILJS_SERVICE_ID
  const TEMPLATE_ID = import.meta.env.APP_EMAILJS_TEMPLATE_ID
  const TEMPLATE_ID_CONFIRMATION = import.meta.env.APP_EMAILJS_TEMPLATE_ID_CONFIRMATION
  const PUBLIC_KEY = import.meta.env.APP_EMAILJS_PUBLIC_KEY

  // 1. Send Email to Chisom (You)
  const templateParams = {
    to_name: 'Chisom',
    from_name: 'Effie',
    message: 'Congratulations! Effie said yes and would be your valentine! ❤',
    email: import.meta.env.APP_EMAIL_TO_CHISOM
  }

  emailjs.send(SERVICE_ID, TEMPLATE_ID, templateParams, { publicKey: PUBLIC_KEY })
    .then(() => console.log('Email to Chisom sent!'))
    .catch((err) => console.error('Failed to send to Chisom:', err))

  // 2. Send Email to Effie (Confirmation)
  const effieParams = {
    to_name: 'Effie',
    from_name: 'Chisom',
    message: 'You said YES! I am so happy!',
    email: import.meta.env.APP_EMAIL_TO_EFFIE
  }

  emailjs.send(SERVICE_ID, TEMPLATE_ID_CONFIRMATION, effieParams, { publicKey: PUBLIC_KEY })
    .then(() => console.log('Confirmation to Effie sent!'))
    .catch((err) => console.error('Failed to send to Effie:', err))

  /* 
     Display success message immediately. 
     Emails are sent in background via emailjs. 
  */
}
</script>

<template>
  <div class="valentine-container">
    <PhotoCarousel :images="images" :quotes="quotes" />
    
    <div class="question-container">
      <h1 class="question">Effie, would you be my valentine?</h1>
    </div>

    <div v-if="!showSuccess" class="buttons-container">
      <button 
        class="yes-btn" 
        :style="{ fontSize: `${yesButtonSize * 1.2}rem` }"
        @click="handleYesClick"
      >
        Yes
      </button>
      <button class="no-btn" @click="handleNoClick">
        No
      </button>
    </div>

    <div v-else class="success-message">
      <h2>Yay! ❤</h2>
      <p>I love you so much!</p>
    </div>
  </div>
</template>

<style scoped>
.valentine-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  min-height: 100vh;
  background-color: #fce4ec;
  font-family: 'Georgia', serif;
  text-align: center;
  padding: 20px;
  overflow-x: hidden; /* Prevent horizontal scroll when button gets huge */
}

.question-container {
  animation: pulse 2s infinite;
  margin-bottom: 30px;
}

.question {
  font-size: 2.5rem;
  color: #e91e63;
  margin: 0;
  text-shadow: 2px 2px 4px rgba(0,0,0,0.1);
}

.buttons-container {
  display: flex;
  gap: 20px;
  align-items: center;
  justify-content: center;
  flex-wrap: wrap;
  min-height: 100px; /* Reserve space */
}

button {
  padding: 15px 30px;
  font-size: 1.2rem;
  border: none;
  border-radius: 50px;
  cursor: pointer;
  transition: all 0.3s ease;
  font-family: 'Georgia', serif;
  box-shadow: 0 4px 6px rgba(0,0,0,0.1);
}

.yes-btn {
  background-color: #4caf50;
  color: white;
  z-index: 10; /* Ensure Yes is always on top if they overlap */
}

.yes-btn:hover {
  background-color: #43a047;
}

.no-btn {
  background-color: #f44336;
  color: white;
}

.no-btn:hover {
  background-color: #e53935;
}

.success-message {
  animation: popIn 0.5s ease-out;
}

.success-message h2 {
  font-size: 4rem;
  color: #e91e63;
  margin-bottom: 0;
}

.success-message p {
  font-size: 1.5rem;
  color: #880e4f;
}

@keyframes pulse {
  0% { transform: scale(1); }
  50% { transform: scale(1.05); }
  100% { transform: scale(1); }
}

@keyframes popIn {
  0% { transform: scale(0); opacity: 0; }
  80% { transform: scale(1.1); opacity: 1; }
  100% { transform: scale(1); }
}
</style>
