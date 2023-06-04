<script lang="ts" setup>
import { ref } from "vue"
import { useRouter } from "vue-router"

const username = ref()
const password = ref()
const router = useRouter()

function login() {
  console.log("brenda login")
  console.log("Username: ", username.value)
  console.log("Password: ", password.value)

  if (username.value === "stanley" && password.value === "123456") {
    localStorage.setItem("jwt", "true")
    router.push("/")
  } else {
    localStorage.setItem("jwt", "false")
  }
}
</script>
<template>
  <div class="flex flex-col gap-y-3" @keydown.enter="login()">
    <input
      v-model="username"
      class="w-full rounded-md bg-gray-100 py-2 px-3"
      placeholder="username"
      type="text"
    />
    <input
      v-model="password"
      class="w-full rounded-md bg-gray-100 py-2 px-3"
      placeholder="password"
      type="password"
    />

    <button
      class="block rounded border border-green-500 bg-transparent py-2 px-4 font-semibold text-green-700 hover:border-transparent hover:bg-green-500 hover:text-white"
      @click="login()"
    >
      Sign In
    </button>
  </div>

  <div class="mt-3">
    <span class="text-sm">
      Don't have an account?
      <router-link class="font-bold text-green-700" to="/signup"
        >Sign up here!</router-link
      ></span
    >
  </div>
</template>