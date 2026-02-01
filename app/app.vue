<template>
  <v-app>
    <!-- <v-app-bar app color="pink-lighten-4" elevation="1" light>
      <v-toolbar-title class="text-pink-darken-1 font-weight-bold">
        <v-icon icon="mdi-heart" class="mr-2"></v-icon>
        Lovely App
      </v-toolbar-title>
      <v-spacer></v-spacer>
      <v-btn variant="text" color="pink-darken-1" to="/" class="text-none">Home</v-btn>
      <v-btn variant="text" color="pink-darken-1" to="/about" class="text-none">About</v-btn>
    </v-app-bar> -->

    <v-main class="romantic-container">
      <div class="background-overlay"></div>
      <NuxtPage />
    </v-main>
<!-- 
    <AppFooter /> -->
  </v-app>
</template>

<style>
.romantic-container {
  min-height: 100vh;
  background: linear-gradient(-45deg, #fff5f7, #fee2e2, #fff1f2, #fae8ff);
  background-size: 400% 400%;
  animation: gradient 15s ease infinite;
  position: relative;
  overflow-x: hidden;
}

.background-overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-image: radial-gradient(#f472b6 0.5px, transparent 0.5px);
  background-size: 30px 30px;
  opacity: 0.1;
  pointer-events: none;
}

@keyframes gradient {
  0% {
    background-position: 0% 50%;
  }
  50% {
    background-position: 100% 50%;
  }
  100% {
    background-position: 0% 50%;
  }
}

/* Global transitions for pages */
.page-enter-active,
.page-leave-active {
  transition: all 0.4s;
}
.page-enter-from,
.page-leave-to {
  opacity: 0;
  filter: blur(1rem);
}
</style>
