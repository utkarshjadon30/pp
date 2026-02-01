<template>
  <v-container fluid class="fill-height welcome-container pa-0">
    <!-- Left Top Corner Back Button -->
    <div class="left-top-action">
      <v-btn
        v-motion
        :initial="{ opacity: 0, x: -50 }"
        :enter="{ opacity: 1, x: 0, transition: { delay: 1000, duration: 800 } }"
        variant="text"
        color="pink-lighten-4"
        prepend-icon="mdi-arrow-left"
        class="text-none font-weight-bold"
        to="/"
      >
        Back
      </v-btn>
    </div>

    <!-- Top Corner Button -->
    <div class="top-action">
      <v-btn
        v-motion
        :initial="{ opacity: 0, x: 50 }"
        :enter="{ opacity: 1, x: 0, transition: { delay: 1000, duration: 800 } }"
        color="pink-accent-2"
        size="large"
        class="rounded-pill px-8"
        to="/love-story"
      >
        Continue Love
      </v-btn>
    </div>

    <!-- Centered Video Container -->
    <div 
      v-motion
      :initial="{ opacity: 0, scale: 0.8 }"
      :enter="{ opacity: 1, scale: 1, transition: { duration: 1000, ease: 'easeOut' } }"
      class="video-container-small"
    >
      <video 
        autoplay 
        loop 
        playsinline 
        class="welcome-video"
      >
        <source src="/hearts.mp4" type="video/mp4">
        Your browser does not support the video tag.
      </video>
    </div>
  </v-container>
</template>

<script setup>
// Welcome page logic
</script>

<style scoped>
.welcome-container {
  height: 100vh;
  background: black;
  overflow: hidden;
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
}

.top-action {
  position: absolute;
  top: 2rem;
  right: 2rem;
  z-index: 10;
}

.left-top-action {
  position: absolute;
  top: 2rem;
  left: 2rem;
  z-index: 10;
}

.video-container-small {
  width: 90%;
  max-width: 900px;
  height: 80vh;
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
  border-radius: 2rem;
  overflow: hidden;
  box-shadow: 0 20px 50px rgba(0, 0, 0, 0.5);
  border: 2px solid rgba(255, 182, 193, 0.3);
}

.welcome-video {
  width: 100%;
  height: 100%;
  object-fit: cover;
}
</style>
