<template>
  <div class="flex flex-col gap-y-3" @keydown.enter="registerUser">
    <small v-show="emailError">Email is not in the correct format.</small>
    <input type="text" id="username" v-model="username" required class="w-full rounded-md bg-gray-100 py-2 px-3" placeholder="Username" />
    <input type="email" id="email" v-model="email" @blur="validateEmail" required class="w-full rounded-md bg-gray-100 py-2 px-3" placeholder="Email" />
    <span v-if="emailError" style="color: red">{{ emailError }}</span>
    <input type="password" id="password" v-model="password" required class="w-full rounded-md bg-gray-100 py-2 px-3" placeholder="Password" /> 
    <button class="block rounded border border-green-500 bg-transparent py-2 px-4 font-semibold text-green-700 hover:border-transparent hover:bg-green-500 hover:text-white" @click="registerUser">
      Sign up
    </button>
    <div v-if="registrationMessage">{{ registrationMessage }}</div>
  </div>
   <div class="mt-3">
    <span class="text-sm">
      Already registered?
      <router-link class="font-bold text-green-700" to="/login">Sign in here!</router-link>
    </span>
  </div>
</template>
 <script>
import axios from 'axios';
import { ref } from "vue";
import { useRouter } from "vue-router";
import { baseURL } from "@/utils/constants";
 export default {
  name: 'Regist',
  setup() {
    const username = ref('');
    const email = ref('');
    const password = ref('');
    const emailError = ref('');
    const registrationMessage = ref('');
     const router = useRouter();
     async function registerUser() {
      try {
        const response = await fetch('/signup', {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json',
          },
          body: JSON.stringify({
            username: username.value,
            email: email.value,
            password: password.value,
          }),
        })
         if (response.ok) {
          const responseData = await response.json()
          registrationMessage.value = responseData.message
        } else if (response.status === 409) {
          const responseData = await response.json()
          emailError.value = ''
          registrationMessage.value = ''
          alert(responseData.message);
        } else {
          console.error('Failed to register user')
        }
      } catch (error) {
        console.error(error)
      }
    }
     async function validateEmail() {
      const emailRegex = /^\S+@\S+\.\S+$/
      if (!emailRegex.test(email.value)) {
        emailError.value = 'Invalid email format'
      } else {
        emailError.value = ''
      }
    }
     return {
      username,
      email,
      password,
      emailError,
      registrationMessage,
      registerUser,
      validateEmail
    };
  }
}
</script>