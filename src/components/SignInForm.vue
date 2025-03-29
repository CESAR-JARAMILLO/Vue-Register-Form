<!-- SignInForm.vue -->
<script setup>
import { ref, reactive } from "vue";

// Form State
const form = reactive({
  email: "",
  password: "",
});

// UI State
const errors = reactive({});
const isSubmitting = ref(false);
const authError = ref("");

// Validation function
const validateForm = () => {
  errors.email = !form.email ? "Email is required" : "";
  errors.password = !form.password ? "Password is required" : "";

  // Optional: Validate email format
  if (form.email && !/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(form.email)) {
    errors.email = "Email is invalid";
  }

  // Return true if no errors
  return !Object.values(errors).some((error) => error);
};

// Sign in function (simulated API call)
const signIn = async () => {
  authError.value = ""; // Reset any previous auth error

  // Validate form before submission
  if (!validateForm()) return;

  isSubmitting.value = true;

  try {
    // Simulate API call (using a 1500ms delay)
    await new Promise((resolve) => setTimeout(resolve, 1500));

    form.email = "";
    form.password = "";

    // Simulate successful sign in
    console.log("Sign in simulated successfully", { ...form });

    // Optionally, you could clear the form or perform additional logic here
  } catch (error) {
    console.error("Error signing in:", error);
    authError.value = "Sign in failed. Please try again.";
  } finally {
    isSubmitting.value = false;
  }
};
</script>

<template>
  <h2 class="text-2xl font-bold text-gray-800 mb-6">Sign In</h2>
  <form @submit.prevent="signIn" class="space-y-6">
    <div>
      <label for="email" class="block text-sm font-medium text-gray-700 mb-1"
        >Email Address</label
      >
      <input
        v-model="form.email"
        id="email"
        type="email"
        class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-primary-500 focus:border-primary-500 transition-colors"
        :class="{ 'border-red-500': errors.email }"
        placeholder="john@example.com"
      />
      <p v-if="errors.email" class="mt-1 text-sm text-red-600">
        {{ errors.email }}
      </p>
    </div>

    <div>
      <label for="password" class="block text-sm font-medium text-gray-700 mb-1"
        >Password</label
      >
      <input
        v-model="form.password"
        id="password"
        type="password"
        class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-primary-500 focus:border-primary-500 transition-colors"
        :class="{ 'border-red-500': errors.password }"
        placeholder="••••••••"
      />
      <p v-if="errors.password" class="mt-1 text-sm text-red-600">
        {{ errors.password }}
      </p>
    </div>

    <button
      type="submit"
      class="w-full flex justify-center py-2 px-4 border border-transparent rounded-lg shadow-sm text-sm font-medium text-white bg-primary-600 hover:bg-primary-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-primary-500 transition-colors cursor-pointer"
      :disabled="isSubmitting"
    >
      <span v-if="isSubmitting">Signing In...</span>
      <span v-else>Sign In</span>
    </button>

    <p v-if="authError" class="text-sm text-red-600 text-center">
      {{ authError }}
    </p>
  </form>
</template>

<style>
:root {
  --color-primary-500: #8b5cf6;
  --color-primary-600: #7c3aed;
  --color-primary-700: #6d28d9;
}

.text-primary-500 {
  color: var(--color-primary-500);
}
.text-primary-600 {
  color: var(--color-primary-600);
}
.hover\:text-primary-500:hover {
  color: var(--color-primary-500);
}
.hover\:text-primary-700:hover {
  color: var(--color-primary-700);
}

.bg-primary-600 {
  background-color: var(--color-primary-600);
}
.hover\:bg-primary-700:hover {
  background-color: var(--color-primary-700);
}

.border-primary-500 {
  border-color: var(--color-primary-500);
}

.focus\:ring-primary-500:focus {
  --tw-ring-color: var(--color-primary-500);
}
.focus\:border-primary-500:focus {
  border-color: var(--color-primary-500);
}
</style>
