<script setup>
import { useCurrentUser, useFirebaseAuth } from 'vuefire'
import { signOut } from 'firebase/auth'

const user = useCurrentUser()
const auth = useFirebaseAuth()

function signOutOfFirebase() {
  signOut(auth)
    .then(() => {
      console.log('Logged out!')
    })
    .catch((error) => {
      console.log(error)
    })
}
</script>

<template>
  <v-app-bar color="teal">
    <v-app-bar-title>Vue Eats</v-app-bar-title>
    <v-spacer></v-spacer>
    <nav class="pr-4">
      <v-btn to="/">Home</v-btn>
      <v-btn to="/new">New</v-btn>
      <v-btn v-if="user?.email" @click="signOutOfFirebase">Sign Out</v-btn>
      <v-btn v-else to="/sign-in">Sign-In</v-btn>
    </nav>
  </v-app-bar>
</template>

<style></style>
