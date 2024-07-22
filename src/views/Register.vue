<template>
  <div class="bg-blue-900 text-white py-4 shadow-md">
    <div class="max-w-md mx-auto flex justify-between items-center">
      <router-link to="/" class="text-xl font-semibold">Welcome</router-link>
      <router-link to="/login"  class="bg-white text-gray-900 font-semibold py-2 px-4 rounded hover:bg-gray-200 focus:outline-none focus:shadow-outline">
        Get Started
      </router-link>
     </div>
  </div>
  <div class="flex items-center justify-center min-h-screen">    
    <form @submit.prevent="registerLecturer" class="w-full max-w-sm bg-white shadow-md rounded px-8 pt-6 pb-8 mb-4">
      <h1 class="py-6 text-2xl font-semibold">Registration Form</h1>
      <div class="mb-4">
        <label class="block text-gray-700 text-sm font-bold mb-2" for="email">
          Email Address
        </label>
        <input v-model="form.email" id="email" name="email" type="email" required class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline">
      </div>
      <div class="mb-6">
        <label class="block text-gray-700 text-sm font-bold mb-2" for="password">
          Password
        </label>
        <input v-model="form.password" id="password" name="password" type="password" required class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline">
      </div>
      <div class="flex items-center justify-between">
        <button type="submit" class="bg-blue-900 hover:bg-blue-800 text-white font-semibold py-2 px-4 rounded focus:outline-none focus:shadow-outline">
          Register
        </button>
        <router-link to="/login" class="inline-block align-baseline font-bold text-sm text-blue-800 underline">click to login</router-link>
      </div>
    </form>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      form: {
        email: '',
        password: '',
      },
    };
  },
  methods: {
    async registerLecturer() {
      try {
        await axios.post('https://labfront-api.onrender.com/api/lecturer/register', this.form);
        alert('User registered successfully');
        this.$router.push('/login');
      } catch (error) {
        alert('Error registering');
        console.error(error);
      }
    },
  },
};
</script>

<style>
/* Tailwind CSS classes can be used directly in your components */
</style>
