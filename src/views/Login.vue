<script setup lang="ts">
import { reactive } from "vue";
import { useRouter } from "vue-router";

import { signInWithEmailAndPassword } from "@firebase/auth";
import { auth } from "@/plugins/firebase";

const router = useRouter();

const form = reactive({
  email: "",
  password: "",
});

const login = async () => {
  try {
    await signInWithEmailAndPassword(auth, form.email, form.password);

    router.push({ name: "Dashboard" });
  } catch (error) {
    //
  }
};
</script>

<template>
  <h1>Login</h1>
  <v-form @submit.prevent="login">
    <v-text-field
      v-model="form.email"
      type="email"
      placeholder="john.doe@mail.com"
    />
    <v-text-field
      v-model="form.password"
      type="password"
      placeholder="******"
    />
    <v-btn type="submit" block>submit</v-btn>
  </v-form>
</template>
