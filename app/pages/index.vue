<template>
  <v-container fluid class="fill-height love-container">
    <v-row align="center" justify="center">
      <v-col cols="12" sm="10" md="6" lg="5" xl="4">
        <!-- Main Card with Motion Animation -->
        <v-card
          v-motion
          :initial="{ opacity: 0, y: 100, scale: 0.9 }"
          :enter="{ opacity: 1, y: 0, scale: 1, transition: { type: 'spring', stiffness: 250, damping: 25, mass: 0.5 } }"
          class="elevation-12 rounded-xl overflow-hidden login-card mx-auto"
        >
          <div class="heart-container py-6 text-center">
            <v-icon
              v-motion
              :initial="{ scale: 1 }"
              :enter="{ 
                scale: [1, 1.2, 1],
                transition: { 
                  repeat: Infinity, 
                  duration: 2000,
                  ease: 'easeInOut'
                } 
              }"
              icon="mdi-heart"
              color="pink-accent-1"
              size="80"
            ></v-icon>
          </div>

          <v-card-text class="px-6 px-sm-10 pb-10">
            <h1 class="text-h4 font-weight-bold text-center mb-2 text-pink-darken-1">Access Restrict-ed! 🤫</h1>
            <p class="text-subtitle-1 text-center mb-8 text-pink-lighten-2">Entrance only for the official 'Prachibot'. Unauthorized cuteness will be prosecuted! 👮‍♀️💖</p>

            <v-form @submit.prevent="handleLogin">
              <v-text-field
                v-model="username"
                label="Your Sweet Username"
                prepend-inner-icon="mdi-account-heart-outline"
                variant="outlined"
                color="pink-lighten-2"
                class="rounded-lg mb-2"
                required
              ></v-text-field>

              <v-text-field
                v-model="password"
                label="Secret Love Password"
                prepend-inner-icon="mdi-lock-outline"
                :append-inner-icon="showPassword ? 'mdi-eye' : 'mdi-eye-off'"
                :type="showPassword ? 'text' : 'password'"
                variant="outlined"
                color="pink-lighten-2"
                class="rounded-lg mb-6"
                required
                @click:append-inner="showPassword = !showPassword"
              ></v-text-field>

              <v-btn
                block
                size="x-large"
                color="pink-accent-2"
                class="text-white font-weight-bold rounded-lg elevation-4 mb-4 login-btn"
                type="submit"
                :loading="loading"
              >
                <span class="text-wrap">Are u Suarr you want to enter?</span>
              </v-btn>

              <div class="text-center">
                <v-btn variant="text" color="pink-lighten-2" class="text-none" @click="showHint = true">
                  Forgot Secret?
                </v-btn>
              </div>

              <v-expand-transition>
                <div v-if="showHint" class="text-center mt-2 text-pink-darken-2 font-weight-medium">
                  Hint: Dhaba + candy 🍭
                </div>
              </v-expand-transition>
            </v-form>
          </v-card-text>
        </v-card>
      </v-col>
    </v-row>

    <!-- Floating Hearts in Background -->
    <div class="floating-hearts">
      <v-icon
        v-for="n in 12"
        :key="n"
        icon="mdi-heart"
        :style="heartStyles[n-1]"
        class="floating-heart"
      ></v-icon>
    </div>
  </v-container>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const username = ref('')
const password = ref('')
const loading = ref(false)
const showHint = ref(false)
const showPassword = ref(false)

const handleLogin = () => {
  if (username.value === 'prachibot' && password.value === 'kissme') {
    loading.value = true
    setTimeout(() => {
      loading.value = false
      navigateTo('/welcome')
    }, 1500)
  } else {
    alert('Incorrect secret, try again with love! 💔')
  }
}

// Random styles for background floating hearts
const heartStyles = ref([])

onMounted(() => {
  heartStyles.value = Array.from({ length: 12 }, () => ({
    top: `${Math.random() * 100}%`,
    left: `${Math.random() * 100}%`,
    fontSize: `${10 + Math.random() * 30}px`,
    opacity: 0.1 + Math.random() * 0.3,
    animationDuration: `${10 + Math.random() * 20}s`,
    animationDelay: `${Math.random() * 10}s`
  }))
})
</script>

<style scoped>
.love-container {
  position: relative;
  overflow: hidden;
  min-height: calc(100vh - 64px); /* Subtracting app bar height */
}

.heart-container {
  background: rgba(255, 255, 255, 0.3);
}

.floating-hearts {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  pointer-events: none;
  z-index: 0;
}

.floating-heart {
  position: absolute;
  color: #f472b6;
  animation: float 20s infinite linear;
}

@keyframes float {
  0% {
    transform: translateY(0) rotate(0deg);
  }
  50% {
    transform: translateY(-100px) rotate(180deg);
  }
  100% {
    transform: translateY(0) rotate(360deg);
  }
}

:deep(.v-card).login-card {
  backdrop-filter: blur(8px);
  background-color: rgba(255, 255, 255, 0.85) !important;
  border: 1px solid rgba(255, 182, 193, 0.3);
  max-width: 550px;
  width: 100%;
}

.login-btn {
  height: auto !important;
  min-height: 56px;
  padding: 12px 16px !important;
}

.text-wrap {
  white-space: normal;
  line-height: 1.2;
}
</style>
