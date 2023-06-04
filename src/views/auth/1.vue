<template>
  <div class="flex flex-col gap-y-3" @keydown.enter="login">
    <input type="email" id="email" v-model="email" required class="w-full rounded-md bg-gray-100 py-2 px-3" placeholder="Email" />
    <input type="password" id="password" v-model="password" required class="w-full rounded-md bg-gray-100 py-2 px-3" placeholder="Password" /> 
    <div v-if="loginMessage">{{ loginMessage }}</div>
    <button class="block rounded border border-green-500 bg-transparent py-2 px-4 font-semibold text-green-700 hover:border-transparent hover:bg-green-500 hover:text-white" @click="login">
      Sign in
    </button>
  </div>
  <div class="mt-3">
    <span class="text-sm">
      Don't have an account? 
      <router-link class="font-bold text-green-700" to="/regist">Sign up here!</router-link>
    </span>
  </div>
</template>
 <script>
import { ref } from "vue";
import { useRouter } from "vue-router";
import { baseURL } from "@/utils/constants";
 export default {
  name: "login",
  setup() {
    const email = ref("");
    const password = ref("");
    const loginMessage = ref("");
    const router = useRouter();
     async function login() {
      try {
        const response = await fetch(`${baseURL}/signin`, {
          method: "POST",
          headers: {
            "Content-Type": "application/json"
          },
          body: JSON.stringify({
            email: email.value,
            password: password.value,
          })
        });
        if (response.ok) {
          const responseData = await response.json();
          localStorage.setItem('token', responseData.token);
          loginMessage.value = "";
          router.push("/");
        } else if (response.status === 401) {
          const responseData = await response.json()
          loginMessage.value = responseData.message
        } else {
          console.error("Failed to login user");
        }
      } catch (error) {
        console.error(error);
      }
    }
     return {
      email,
      password,
      loginMessage,
      login
    };
  }
};
</script>