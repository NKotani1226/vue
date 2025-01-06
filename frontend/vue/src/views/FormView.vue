<template>
  <div class="form">
    <form @submit.prevent="validateForm">
    <div>
      <label>Email:</label>
      <input v-model="email" type="email" />
      <p class="red" v-if="errors.email">{{ errors.email }}</p>
    </div>
    <div>
      <label>Password:</label>
      <input v-model="password" type="password" />
      <p class="red" v-if="errors.password">{{ errors.password }}</p>
    </div>
    <button type="submit">Submit</button>
  </form>
  </div>
</template>

<style>
@media (min-width: 1024px) {
  .form {
    min-height: 100vh;
    display: flex;
    align-items: center;
  }
  .red {
    color: red;
  }
}
</style>

<script>
import { ref } from "vue";

export default {
  setup() {
    const email = ref("");
    const password = ref("");
    const errors = ref({});

    const validateForm = () => {
      errors.value = {};
      if (!email.value) {
        errors.value.email = "Email is required.";
      } else if (!/^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$/.test(email.value)) {
        errors.value.email = "Email must be valid.";
      }

      if (!password.value) {
        errors.value.password = "Password is required.";
      } else if (password.value.length < 6) {
        errors.value.password = "Password must be at least 6 characters.";
      }

      if (!Object.keys(errors.value).length) {
        alert("Form submitted successfully!");
      }
    };

    return {
      email,
      password,
      errors,
      validateForm,
    };
  },
};
</script>