<template>
  <v-footer color="rgba(255, 255, 255, 0.3)" class="mt-8" style="backdrop-filter: blur(5px);">
    <v-container>
      <v-row justify="center" no-gutters>
        <v-btn
          v-for="link in links"
          :key="link"
          color="primary"
          variant="text"
          class="mx-2"
          rounded="xl"
        >
          {{ link }}
        </v-btn>
        <v-col class="text-center mt-4" cols="12">
          {{ new Date().getFullYear() }} — <strong>My Nuxt App</strong>
        </v-col>
      </v-row>
    </v-container>
  </v-footer>
</template>

<script setup>
const links = [
  'Home',
  'About Us',
  'Team',
  'Services',
  'Blog',
  'Contact Us',
]
</script>
