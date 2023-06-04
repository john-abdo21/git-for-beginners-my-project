<script lang="ts" setup>
import PayRoll from "@/components/Reports/PayRoll.vue"
import Taxes from "@/components/Reports/Taxes.vue"
import Timesheet from "@/components/Reports/Timesheet.vue"
import Employee from "@/components/Reports/Employee.vue"
</script>

<template>
  <div class="flex h-full w-full justify-center">
    <div
      class="flex h-full w-full max-w-7xl flex-col self-center overflow-y-scroll rounded bg-white py-4 px-10 pb-16 shadow dark:bg-primary-gray-dark"
    >
      <div class="flex w-full flex-col gap-y-6 py-3 px-16">
        <PayRoll />
        <Taxes />
        <Timesheet />
        <Employee />
      </div>
    </div>
  </div>
</template>