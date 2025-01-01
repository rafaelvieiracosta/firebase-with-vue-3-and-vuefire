<script setup>
import { ref } from 'vue'

import { useFirebaseAuth } from 'vuefire'

import {
  createUserWithEmailAndPassword,
  signInWithEmailAndPassword,
} from 'firebase/auth'

import BaseButton from '@/components/base/BaseButton.vue'
import BaseContainer from '@/components/base/BaseContainer.vue'
import BaseCard from '@/components/base/BaseCard.vue'
import BaseForm from '@/components/base/BaseForm.vue'
import BaseInput from '@/components/base/BaseInput.vue'

const userInput = ref({
  email: '',
  password: '',
})

const auth = useFirebaseAuth()

async function createUser() {
  createUserWithEmailAndPassword(
    auth,
    userInput.value.email,
    userInput.value.password
  )
    .then((userCredential) => {
      const user = userCredential.user
      console.log(user)
    })
    .catch((error) => {
      console.log(error)
    })
}

async function signInToFirebase() {
  signInWithEmailAndPassword(
    auth,
    userInput.value.email,
    userInput.value.password
  )
    .then((userCredential) => {
      const user = userCredential.user
      console.log(user)
    })
    .catch((error) => {
      console.log(error)
    })
}
</script>

<template>
  <BaseContainer>
    <h1 class="mb-4">Sign In</h1>
    <BaseCard>
      <template v-slot:default>
        <BaseForm>
          <BaseInput
            v-model="userInput.email"
            type="email"
            label="Email"
            required
            placeholder="eleanorshellstrop@thegoodplace.com"
          />
          <BaseInput
            v-model="userInput.password"
            label="Password"
            type="password"
            required
          />
        </BaseForm>
      </template>
      <template v-slot:actions>
        <BaseButton variant="tonal" color="success" @click="signInToFirebase">
          Sign In
        </BaseButton>

        <BaseButton
          variant="tonal"
          color="secondary"
          outline
          @click="createUser"
        >
          Create New User
        </BaseButton>
      </template>
    </BaseCard>
  </BaseContainer>
</template>

<style></style>
