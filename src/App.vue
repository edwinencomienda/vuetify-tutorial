<template>
  <v-app>
    <v-toolbar class="elevation-1" color="indigo" dark app>
      <v-toolbar-title class="text-uppercase">
        <span>Vuetify Tutorial</span>
      </v-toolbar-title>
      <v-spacer></v-spacer>
      <v-btn flat to="/">Home</v-btn>
      <v-btn flat to="/about">About</v-btn>
    </v-toolbar>

    <v-content>
      <v-container>
        <router-view></router-view>
      </v-container>
    </v-content>
  </v-app>
</template>

<script>

export default {
  name: 'App'
}
</script>
