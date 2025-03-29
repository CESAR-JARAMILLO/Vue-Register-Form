<script setup>
import RegisterForm from "./components/RegisterForm.vue";
import SignInForm from "./components/SignInForm.vue";
import { ref } from "vue";

const registerView = ref(false);
</script>

<template>
  <div class="min-h-screen bg-gray-50 flex items-center justify-center p-4">
    <div class="max-w-md w-full bg-white rounded-xl shadow-lg p-8">
      <RegisterForm v-if="registerView" />
      <SignInForm v-else />

      <div class="mt-6 text-center">
        <p class="text-sm text-gray-600">
          {{ registerView ? "Already" : "Don't" }} have an account?

          <a
            href="#"
            class="font-medium text-primary-600 hover:text-primary-500"
            @click="registerView = !registerView"
            >{{ registerView ? "Sign in" : "Register" }}</a
          >
        </p>
      </div>
    </div>
  </div>
</template>

<style scoped>
</style>
