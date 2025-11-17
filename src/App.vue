<template>
  <v-app>
    <!-- Navigation -->
    <v-app-bar
      elevation="0"
      color="grey-lighten-4"
      class="px-4"
    >
      <v-app-bar-title class="text-grey-darken-2 text-h6 d-none d-sm-flex">JONAS VAGNER RIIS</v-app-bar-title>
      <v-app-bar-title class="text-grey-darken-2 text-subtitle-1 d-flex d-sm-none">JONAS VAGNER RIIS</v-app-bar-title>
      <v-spacer></v-spacer>
      
      <!-- Desktop Navigation -->
      <div class="d-none d-sm-flex">
        <v-btn variant="text" class="text-grey-darken-2" @click="scrollToSection('hero')">Home</v-btn>
        <v-btn variant="text" class="text-grey-darken-2" @click="scrollToSection('about')">About</v-btn>
        <v-btn variant="text" class="text-grey-darken-2" @click="scrollToSection('cases')">Cases</v-btn>
      </div>
      
      <!-- Mobile Navigation Button -->
      <v-app-bar-nav-icon
        class="d-flex d-sm-none"
        @click="drawer = !drawer"
      ></v-app-bar-nav-icon>
    </v-app-bar>

    <!-- Mobile Navigation Drawer -->
    <v-navigation-drawer
      v-model="drawer"
      temporary
      location="right"
    >
      <v-list>
        <v-list-item @click="scrollToSection('hero'); drawer = false">
          <v-list-item-title>Home</v-list-item-title>
        </v-list-item>
        <v-list-item @click="scrollToSection('about'); drawer = false">
          <v-list-item-title>About</v-list-item-title>
        </v-list-item>
        <v-list-item @click="scrollToSection('cases'); drawer = false">
          <v-list-item-title>Cases</v-list-item-title>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <!-- Main Content -->
    <v-main class="bg-grey-lighten-4">
      <router-view></router-view>
    </v-main>

    <!-- Footer -->
    <v-footer class="bg-white text-grey-darken-2">
      <v-row justify="center" no-gutters>
        <v-col class="text-center py-4" cols="12">
          {{ new Date().getFullYear() }} — <strong>Jonas Vagner Riis</strong>
        </v-col>
      </v-row>
    </v-footer>
  </v-app>
</template>

<script>
// NO IMPORTS HERE
export default {
  name: 'App',
  data: () => ({
    drawer: false,
  }),
  methods: {
    async scrollToSection(sectionId) {
      if (this.$route.path !== '/') {
        await this.$router.push('/')
        // Wait a brief moment for the component to mount
        setTimeout(() => {
          const element = document.getElementById(sectionId)
          if (element) {
            element.scrollIntoView({ 
              behavior: 'smooth',
              block: 'start'
            })
          }
        }, 100)
      } else {
        const element = document.getElementById(sectionId)
        if (element) {
          element.scrollIntoView({ 
            behavior: 'smooth',
            block: 'start'
          })
        }
      }
    }
  }
}
</script>

<style>
.v-application {
  font-family: 'Inter', sans-serif !important;
}
</style>