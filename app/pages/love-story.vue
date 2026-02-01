<template>
  <v-container fluid class="fill-height story-container py-12">
    <!-- Back Button -->
    <div class="top-left-back">
      <v-btn
        variant="text"
        color="pink-darken-1"
        prepend-icon="mdi-arrow-left"
        to="/welcome"
        class="text-none font-weight-bold"
      >
        Back to Welcome
      </v-btn>
    </div>

    <!-- Music Player Indicator (Visual Only) -->
    <div class="music-note" v-motion :initial="{ opacity: 0 }" :enter="{ opacity: 1, transition: { repeat: Infinity, duration: 2000 } }">
      <v-icon icon="mdi-music-note" color="pink-accent-2" size="x-large"></v-icon>
      <span class="text-caption text-pink-darken-1 ml-2">Playing: Pretty Little Baby</span>
    </div>

    <v-row justify="center" align="center">
      <v-col cols="12" md="8" lg="6">
        <v-card
          v-motion
          :initial="{ opacity: 0, y: 50 }"
          :enter="{ opacity: 1, y: 0, transition: { duration: 1000 } }"
          class="love-story-card pa-8 pa-sm-12 text-center rounded-xl"
        >
          <v-icon icon="mdi-heart-multiple" color="pink-accent-1" size="80" class="mb-6"></v-icon>
          
          <h1 class="text-h3 font-weight-bold text-pink-darken-2 mb-6">Where Magic Began...</h1>
          
          <p class="text-h6 text-pink-lighten-1 font-italic mb-8 lh-lg">
            "Some journeys are defined by miles, but ours was defined by moments. It started with a trip filled with laughter and pure fun, where we bonded in ways I never expected. Amidst the magic of the camping site, under a sky full of stars, we found something beautiful in each other. That first kiss wasn't just a spark—it was the moment I knew you were the one."
          </p>

          <v-divider class="mb-8"></v-divider>

          <v-row class="mb-8">
            <v-col 
              v-for="(photo, index) in prachiPhotos" 
              :key="index" 
              cols="6" 
              sm="4"
            >
              <v-hover v-slot="{ isHovering, props }">
                <v-card
                  v-bind="props"
                  :elevation="isHovering ? 12 : 2"
                  class="rounded-lg overflow-hidden transition-swing clickable-card"
                  @click="openPreview(photo)"
                >
                  <v-img
                    :src="`/prachi/${photo}`"
                    cover
                    aspect-ratio="1"
                    class="align-end"
                  >
                    <v-expand-transition>
                      <div
                        v-if="isHovering"
                        class="d-flex transition-fast-in-fast-out bg-pink-accent-1 v-card--reveal text-h2 text-white"
                        style="height: 100%; opacity: 0.4;"
                      >
                        <v-icon icon="mdi-heart" size="large"></v-icon>
                      </div>
                    </v-expand-transition>
                  </v-img>
                </v-card>
              </v-hover>
            </v-col>
          </v-row>

          <v-divider class="my-10"></v-divider>

          <!-- Envelope Section -->
          <div v-if="!proposalAccepted" class="proposal-container py-6">
            <div v-if="!envelopeOpened" class="envelope-wrapper text-center">
              <h3 class="text-h5 text-pink-darken-1 mb-6">Prachi, I have a secret for you...</h3>
              <div 
                v-motion
                :initial="{ scale: 0.9 }"
                :hovered="{ scale: 1.05 }"
                class="envelope-box cursor-pointer"
                @click="envelopeOpened = true"
              >
                <v-icon 
                  icon="mdi-email-heart-outline" 
                  color="pink-accent-1" 
                  size="120"
                ></v-icon>
                <div class="text-subtitle-1 text-pink-lighten-2 mt-2 font-weight-bold">Open this envelope 💌</div>
              </div>
            </div>

            <!-- Proposal Section (shown when envelope is opened) -->
            <v-expand-transition>
              <div v-if="envelopeOpened" class="proposal-section">
                <h2 
                  v-motion
                  :initial="{ scale: 0.9, opacity: 0 }"
                  :enter="{ scale: 1, opacity: 1, transition: { duration: 1000 } }"
                  class="text-h4 font-weight-bold text-pink-darken-3 mb-8"
                >
                  Prachi Arya,I don’t care who your first love was; I intend to be your last.
                  Will you be my headache forever? 💍
                </h2>
                
                <div class="d-flex justify-center align-center gap-4 flex-wrap">
                  <v-btn
                    v-motion
                    :hovered="{ scale: 1.1 }"
                    color="pink-accent-2"
                    size="x-large"
                    class="rounded-pill px-12 elevation-8"
                    @click="acceptProposal"
                  >
                    Ofcourse, I will! ❤️
                  </v-btn>

                  <v-btn
                    ref="noBtn"
                    variant="outlined"
                    color="pink-lighten-2"
                    size="x-large"
                    class="rounded-pill px-10 no-button"
                    :style="noBtnStyle"
                    @mouseover="moveNoButton"
                    @click="moveNoButton"
                  >
                    No 😢
                  </v-btn>
                </div>
              </div>
            </v-expand-transition>
          </div>

          <!-- Success State -->
          <div v-else class="success-section py-10" v-motion :initial="{ scale: 0.5, opacity: 0 }" :enter="{ scale: 1, opacity: 1 }">
            <div class="barca-theme mb-6">
              <v-icon icon="mdi-soccer" color="blue-darken-4" size="60"></v-icon>
              <v-icon icon="mdi-heart" color="red-darken-4" size="40" class="mx-2"></v-icon>
              <v-icon icon="mdi-soccer" color="red-darken-4" size="60"></v-icon>
            </div>
            <h2 class="text-h3 font-weight-bold barca-text mb-4">Visca el Barça! ❤️�</h2>
            <p class="text-h6 text-pink-darken-1 mb-8">
              I’m an FC Barcelona man through and through, and now I finally have the perfect partner to watch my team with. My heart and my team, all in one place!
            </p>
            
            <div class="success-video-wrapper mx-auto elevation-12 rounded-xl overflow-hidden mb-6" style="max-width: 500px; border: 3px solid #f471b633;">
              <v-img
                src="/prachi/messi-kiss-lionel-messi.gif"
                alt="Messi Love"
                cover
                class="rounded-xl"
              ></v-img>
            </div>
          </div>
        </v-card>
      </v-col>
    </v-row>

    <!-- Hidden Audio Player -->
    <audio 
      ref="audioPlayer" 
      src="/Conny_Francis_-_Pretty_Little_Baby_(mp3.pm).mp3" 
      autoplay 
      loop
    ></audio>

    <!-- Fun No Sound Player -->
    <audio 
      ref="noSoundPlayer" 
      src="/sound/fahhh_KcgAXfs.mp3"
    ></audio>

    <!-- Image Preview Dialog -->
    <v-dialog v-model="previewDialog" max-width="90vw" max-height="90vh">
      <v-card class="rounded-xl overflow-hidden bg-transparent" elevation="0">
        <v-btn
          icon="mdi-close"
          position="absolute"
          style="top: 1rem; right: 1rem; z-index: 10;"
          color="white"
          variant="tonal"
          @click="previewDialog = false"
        ></v-btn>
        <v-img
          :src="selectedImage"
          max-height="85vh"
          contain
          class="bg-black"
        ></v-img>
      </v-card>
    </v-dialog>
  </v-container>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const audioPlayer = ref(null)
const noSoundPlayer = ref(null)
const previewDialog = ref(false)
const selectedImage = ref('')
const proposalAccepted = ref(false)
const envelopeOpened = ref(false)
const noBtnStyle = ref({ position: 'relative', left: '0', top: '0' })

const prachiPhotos = [
  'IMG_2484.JPG',
  'IMG_2594.JPG',
  'IMG_2599.JPG',
  'IMG_2765.JPG',
  'WhatsApp Image 2026-01-26 at 02.38.07.jpeg',
  'WhatsApp Image 2026-01-27 at 15.53.07.jpeg'
]

const openPreview = (photo) => {
  selectedImage.value = `/prachi/${photo}`
  previewDialog.value = true
}

const acceptProposal = () => {
  proposalAccepted.value = true
}

const isMoving = ref(false)

const moveNoButton = () => {
  if (isMoving.value) return
  
  isMoving.value = true
  
  // Play funny sound with debounce check
  if (noSoundPlayer.value) {
    noSoundPlayer.value.volume = 1.0
    // Always restart for maximum effect on interaction
    noSoundPlayer.value.currentTime = 0
    noSoundPlayer.value.play().catch(e => console.log("Sound play blocked"))
  }

  // Increase range for mobile so it really "runs away"
  const range = window.innerWidth < 600 ? 250 : 200
  const x = Math.random() * range - (range / 2)
  const y = Math.random() * range - (range / 2)
  
  noBtnStyle.value = {
    position: 'relative',
    left: `${x}px`,
    top: `${y}px`,
    transition: 'all 0.3s ease-out'
  }

  // Cooldown to prevent crazy jumping and sound spam
  setTimeout(() => {
    isMoving.value = false
  }, 300)
}

onMounted(() => {
  if (audioPlayer.value) {
    audioPlayer.value.volume = 0.4 // Set a cozy, low volume
    
    // Attempt to play (browsers might block autoplay without interaction)
    const playPromise = audioPlayer.value.play()
    if (playPromise !== undefined) {
      playPromise.catch(error => {
        console.log("Autoplay was prevented. User interaction required.")
      })
    }
  }
})
</script>

<style scoped>
.story-container {
  background: radial-gradient(circle at center, #fff5f7 0%, #fee2e2 100%);
  min-height: 100vh;
  position: relative;
}

.love-story-card {
  background: rgba(255, 255, 255, 0.7) !important;
  backdrop-filter: blur(15px);
  border: 1px solid rgba(251, 113, 133, 0.2);
  box-shadow: 0 25px 50px -12px rgba(251, 113, 133, 0.25) !important;
}

.top-left-back {
  position: absolute;
  top: 2rem;
  left: 2rem;
  z-index: 10;
}

.music-note {
  position: absolute;
  top: 2rem;
  right: 2rem;
  display: flex;
  align-items: center;
  z-index: 10;
}

.lh-lg {
  line-height: 1.8 !important;
}

.shadow-sm {
  box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1);
}

.clickable-card {
  cursor: pointer;
}

.envelope-box {
  display: inline-block;
  cursor: pointer;
  transition: transform 0.3s ease;
}

.heart-beat {
  animation: beat 1.2s infinite ease-in-out;
}

@keyframes beat {
  0%, 100% { transform: scale(1); }
  50% { transform: scale(1.15); }
}

.gap-4 {
  gap: 1.5rem;
}

.no-button {
  z-index: 5;
}

.barca-text {
  background: linear-gradient(to right, #004D98, #A50044);
  -webkit-background-clip: text;
  background-clip: text;
  -webkit-text-fill-color: transparent;
  display: inline-block;
}

.barca-theme {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 10px;
}
</style>
