<template>
  <v-container>
    <v-row class="mb-10">
      <v-col cols="12" class="text-center">
        <h1 class="text-h2 font-weight-bold text-primary">About Us</h1>
        <div class="text-h5 text-medium-emphasis mt-2">Driven by innovation, crafted for excellence.</div>
      </v-col>
    </v-row>

    <v-row align="center" class="mb-16">
      <v-col cols="12" md="6">
        <v-img
          src="https://picsum.photos/id/1/600/400"
          alt="About Us Image"
          cover
          rounded="lg"
          elevation="4"
        ></v-img>
      </v-col>
      <v-col cols="12" md="6">
        <h2 class="text-h4 mb-4">Our Story</h2>
        <p class="text-body-1 mb-4">
          We started with a simple idea: to make web development accessible and beautiful. 
          Over the years, we've grown into a team of passionate individuals dedicated to 
          creating the best digital experiences for our users.
        </p>
        <p class="text-body-1">
          Each project is a new adventure, and we tackle it with enthusiasm and expertise. 
          From the initial concept to the final deployment, we are there every step of the way.
        </p>
      </v-col>
    </v-row>

    <v-divider class="my-8"></v-divider>

    <v-row>
      <v-col cols="12">
        <h2 class="text-h4 text-center mb-8">Meet the Team</h2>
      </v-col>
      <v-col cols="12" sm="6" md="4" v-for="(member, i) in team" :key="i">
        <v-card variant="outlined" class="text-center pa-4">
          <v-avatar size="120" class="mb-4">
            <v-img :src="member.avatar" alt="Team Member"></v-img>
          </v-avatar>
          <h3 class="text-h6 font-weight-bold">{{ member.name }}</h3>
          <div class="text-subtitle-1 text-primary">{{ member.role }}</div>
          <v-card-text>
            {{ member.bio }}
          </v-card-text>
          <v-card-actions class="justify-center">
            <v-btn icon="mdi-twitter" variant="text" size="small"></v-btn>
            <v-btn icon="mdi-linkedin" variant="text" size="small"></v-btn>
            <v-btn icon="mdi-github" variant="text" size="small"></v-btn>
          </v-card-actions>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script setup>
const team = [
  {
    name: 'Alex Johnson',
    role: 'Lead Developer',
    bio: 'Passionate about Clean Code and Architecture. Loves coffee and hiking.',
    avatar: 'https://i.pravatar.cc/150?u=alex'
  },
  {
    name: 'Sarah Smith',
    role: 'UX Designer',
    bio: 'Believes that design is not just how it looks, but how it works.',
    avatar: 'https://i.pravatar.cc/150?u=sarah'
  },
  {
    name: 'Mike Brown',
    role: 'Product Manager',
    bio: 'Ensuring that we build the right things for the right people.',
    avatar: 'https://i.pravatar.cc/150?u=mike'
  }
]
</script>
