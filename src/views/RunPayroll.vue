<template>
  <div class="flex h-full w-full justify-center">
    <div
      class="flex h-full w-full max-w-7xl flex-col self-center overflow-y-scroll rounded bg-white py-4 px-10 pb-16 shadow dark:bg-primary-gray-dark"
    >
      <!--     Header-->
      <PayrollHeader />

      <!--      Payroll Summary-->
      <PayrollSummary v-if="isRunPayRoll" />

      <!--      Pay Statements-->
      <PayStatementes v-if="isRunPayRoll" />
    </div>
  </div>
</template>

<script lang="ts" setup>
import PayrollHeader from "@/components/RunPayroll/PayrollHeader.vue"
import PayrollSummary from "@/components/RunPayroll/PayrollSummary.vue"
import PayStatementes from "@/components/RunPayroll/PayStatementes.vue"

import { onMounted, ref, onUnmounted } from "vue"
import { storeToRefs } from "pinia"
import { usePayroll } from "@/stores/runPayroll"

const { isRunPayRoll } = storeToRefs(usePayroll())
const store = usePayroll()

// load employees
// const { mountEmployees } = usePayroll()
// mountEmployees()
// const { mountEmployees } = usePayroll()

// const dataEmloyee = store.$state.employees
onUnmounted(() => {
  store.$reset()
})
</script>

<style scoped>
details > summary {
  list-style: none;
}

summary::-webkit-details-marker {
  display: none;
}

summary::after {
  width: 10px;
  content: " ►";
}

details[open] summary:after {
  content: " ▼";
}
</style>