<template>
  <v-app>
    <v-app-bar fixed app class="red accent-3 white--text">
      <v-toolbar-title v-text="'Numbers Memo'" />
    </v-app-bar>
    <v-main>
      <v-container>
        <Nuxt />
      </v-container>
    </v-main>
    <v-footer app>
      <span>&copy; {{ new Date().getFullYear() }}</span>
    </v-footer>
  </v-app>
</template>
