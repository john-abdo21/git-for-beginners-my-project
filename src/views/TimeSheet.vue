<template>
  <div class="flex h-full w-full justify-center">
    <div
      class="flex h-full w-full max-w-5xl flex-col self-center overflow-y-scroll rounded bg-white py-4 px-10 pb-16 shadow dark:bg-primary-gray-dark"
    >
      <div class="mb-8 flex justify-between">
        <div
          class="pb-2 text-2xl font-semibold text-gray-800 dark:text-gray-200"
        >
          Timesheets
        </div>
        <div class="flex items-center">
          <label
            class="block w-[400px] text-lg font-medium text-gray-900 dark:text-gray-400"
            for="paymentType"
            >Select payment type:
          </label>
          <select
            id="paymentType"
            class="block w-full rounded-lg border border-gray-300 bg-gray-50 p-2.5 text-sm text-gray-900 focus:border-blue-500 focus:ring-blue-500 dark:border-gray-600 dark:bg-gray-700 dark:text-white dark:placeholder-gray-400 dark:focus:border-blue-500 dark:focus:ring-blue-500"
            @change="changeComponent($event)"
          >
            <option selected value="WeeklyPayment">Weekly</option>
            <option value="FortnightlyPayment">Fortnightly</option>
            <option value="MonthlyPayment">Monthly</option>
          </select>
        </div>
      </div>
      <div class="mb-4 w-full">
        Add additional hours like overtime, vacation, or sick time by clicking
        the arrow next to employee name. For salaried employees, regular hours
        aren't required.
        <a
          class="inline-flex flex-row items-center font-semibold text-primary"
          href="/"
          >Read Wagez's guide to timesheets
          <span
            class="iconify ml-1 mr-2 h-4 w-4"
            data-icon="ci:external-link"
          />
        </a>
      </div>

      <div>
        <component :is="currentPayment"></component>
      </div>
    </div>
  </div>
</template>

<script>
// import { ref, defineComponent } from "vue"
// import { TabGroup, TabList, Tab, TabPanels, TabPanel } from "@headlessui/vue"
// import TimeSheet from "@/components/TimeSheet/Hourly.vue"

import WeeklyPayment from "@/components/TimeSheet/WeeklyPayment.vue"
import FortnightlyPayment from "@/components/TimeSheet/FortnightlyPayment.vue"
import MonthlyPayment from "@/components/TimeSheet/MonthlyPayment.vue"

export default {
  components: {
    WeeklyPayment,
    FortnightlyPayment,
    MonthlyPayment,
  },
  data() {
    return {
      currentPayment: "WeeklyPayment",
    }
  },
  methods: {
    changeComponent(event) {
      this.currentPayment = event.target.value
    },
  },
}
</script>

<style scoped></style>