<template>
  <div class="flex h-full w-full justify-center">
    <div
      class="flex h-full w-full max-w-7xl flex-col self-center overflow-y-scroll rounded bg-white py-4 px-10 pb-16 shadow dark:bg-primary-gray-dark"
    >
      <!-- Header -->
      <div class="mb-8 flex justify-between">
        <div
          class="pb-2 text-2xl font-semibold text-gray-800 dark:text-gray-200"
        ></div>
      </div>

      <div class="w-full">
        <TabGroup as="div" class="flex flex-row space-x-4" vertical>
          <TabList class="flex w-3/12 flex-col p-1 text-gray-700">
            <Tab
              v-for="category in categories"
              :key="category.label"
              v-slot="{ selected }"
              as="template"
            >
              <button
                :class="[
                  'w-full rounded-lg py-2.5 pl-4 pr-8 text-left text-sm font-medium leading-5 ',
                  selected
                    ? 'bg-primary text-gray-100'
                    : 'text-gray-800 dark:text-gray-200',
                ]"
              >
                <div class="flex items-center">
                  {{ category.label }}
                  <span
                    v-if="category.hasErrors"
                    class="iconify ml-1 h-4 w-4 text-yellow-500"
                    data-icon="bi:exclamation-triangle"
                  />
                </div>
              </button>
            </Tab>
          </TabList>

          <TabPanels class="h-full w-9/12">
            <TabPanel key="General" class="h-full">
              <General />
            </TabPanel>
            <TabPanel key="Personal Information" class="h-full">
              <TaxSettings />
            </TabPanel>
            <TabPanel key="Compensation" class="h-full">
              <PayrollHolidays />
            </TabPanel> 
            <TabPanel key="Holiday" class="h-full">
              <TradeRates />
            </TabPanel>
            <TabPanel key="Other Income & Deductions" class="h-full">
              <OtherincomeDeducetion />
            </TabPanel>
            <TabPanel key="Sick Leaves" class="h-full">
              <SickLeave />
            </TabPanel>
            
            <TabPanel key="Tax Details" class="h-full">
              <Developing />
            </TabPanel>
            <TabPanel key="Benefits & Deductions" class="h-full">
              <Developing />
            </TabPanel>
            <TabPanel key="Employee Files" class="h-full">
              <Developing />
            </TabPanel>
            <TabPanel key="Direct Deposit" class="h-full">
              <PreferenceSettings />
            </TabPanel>
            <TabPanel key="Bank Details" class="h-full">
              <Developing />
            </TabPanel>
            <TabPanel key="Employment Status" class="h-full">
              <Developing />
            </TabPanel>
          </TabPanels>
        </TabGroup>
      </div>
    </div>
  </div>
</template>

<script lang="ts" setup>
import { ref } from "vue"
import { TabGroup, TabList, Tab, TabPanels, TabPanel } from "@headlessui/vue"
import General from "@/components/Settings/General.vue"

import TaxSettings from "@/components/Settings/tax/TaxSettings.vue"
import PayrollHolidays from "@/components/Settings/payroll_holidays/index.vue"
import TradeRates from "@/components/Settings/TradeRates.vue"
import PreferenceSettings from "@/components/Settings/PreferenceSettings.vue"
import OtherincomeDeducetion from '@/components/Settings/OtherIncomeDeductions/otherIcomeDeductions.vue'
import Developing from '@/components/Settings/Developing.vue'

const categories = ref([
  {
    label: "General",
    hasErrors: false,
  },
  {
    label: "Taxes",
    hasErrors: false,
  },
  {
    label: "Payroll Year & Holidays",
    hasErrors: false,
  },
  {
    label: "Trade Rates",
    hasErrors: false,
  },
  {
    label: "Other Income & Deductions",
    hasErrors: false,
  },
  {
    label: "Sick Leaves",
    hasErrors: false,
  },
  
  {
    label: "Job & Bonus",
    hasErrors: false,
  },
  {
    label: "Payment Currency",
    hasErrors: false,
  },
  {
    label: "Payroll General Journal",
    hasErrors: false,
  },
  {
    label: "Preference",
    hasErrors: false,
  },
  {
    label: "Security",
    hasErrors: false,
  },
  {
    label: "Integration Setup",
    hasErrors: false,
  },
  // {
  //   label: "Optional Modules",
  //   hasErrors: false,
  // },
])
</script>
<style scoped></style>
