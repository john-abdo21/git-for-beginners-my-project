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
            <TabPanel key="Attendance & Work" class="h-full">
              <AttendanceWork />
            </TabPanel>
            <TabPanel key="Appraisal Method" class="h-full">
              <AppraisalMethod />
            </TabPanel>
            <TabPanel key="Letter Document" class="h-full">
              <LetterDocument />
            </TabPanel>
            <TabPanel key="Payslip Size" class="h-full">
              <PayslipSize />
            </TabPanel>
            <TabPanel key="Time Clock" class="h-full">
              <TimeClock />
            </TabPanel>
            <TabPanel key="Printer" class="h-full">
              <TimeClock />
            </TabPanel>
            <TabPanel key="Email Communication" class="h-full">
              <TimeClock />
            </TabPanel>
            <TabPanel key="Salary Calulator" class="h-full">
              <SalaryCalculator />
            </TabPanel>
            <TabPanel key="Database Maintenance" class="h-full">
              <TimeClock />
            </TabPanel>
            <TabPanel key="Import data" class="h-full">
              <TimeClock />
            </TabPanel>
            <TabPanel key="Clear unpaid Leave" class="h-full">
              <TimeClock />
            </TabPanel>
            <TabPanel key="Audit Trail" class="h-full">
              <TimeClock />
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
import SalaryCalculator from "@/components/Utilities/SalaryCalculator/SalaryCalculator.vue"
import AttendanceWork from "@/components/Utilities/AttendanceWork.vue"
import AppraisalMethod from "@/components/Utilities/AppraisalMethod.vue"
import PayslipSize from "@/components/Utilities/PayslipSize.vue"
import TimeClock from "@/components/Utilities/TimeClock.vue"
import LetterDocument from "@/components/Utilities/LetterDocument.vue"

const categories = ref([
  {
    label: "Attendance & Work",
    hasErrors: false,
  },
  {
    label: "Appraisal Method",
    hasErrors: false,
  },
  {
    label: "Letter Document",
    hasErrors: false,
  },
  {
    label: "Payslip Size",
    hasErrors: false,
  },
  {
    label: "Time Clock",
    hasErrors: false,
  },
  {
    label: "Printer",
    hasErrors: false,
  },
  {
    label: "Email Communication",
    hasErrors: false,
  },
  {
    label: "Salary Calulator",
    hasErrors: false,
  },
  {
    label: "Database Maintenance",
    hasErrors: false,
  },
  {
    label: "Import data",
    hasErrors: false,
  },
  {
    label: "Clear unpaid Leave",
    hasErrors: false,
  },
  {
    label: "Audit Trail",
    hasErrors: false,
  },
])
</script>
<style scoped></style>
