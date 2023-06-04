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
          >
            <option selected>Weekly</option>
            <option value="US">Fortnightly</option>
            <option value="CA">Monthly</option>
            <option value="FR">Fixed</option>
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
          >Read Wave's guide to timesheets
          <span
            class="iconify ml-1 mr-2 h-4 w-4"
            data-icon="ci:external-link"
          />
        </a>
      </div>
      <div>
        <div
          class="mb-2 text-lg font-semibold text-gray-800 dark:text-gray-200"
        >
          Enter daily hours for the week:
        </div>
        <div
          class="flex w-full items-center rounded border border-primary px-2 py-4"
        >
          <div class="flex w-1/12 justify-center">
            <button
              class="rounded-full font-semibold text-primary hover:bg-primary hover:text-gray-200"
            >
              <span
                class="iconify icon-set"
                data-height="48"
                data-icon="bx:left-arrow-circle"
                data-width="48"
              ></span>
            </button>
          </div>
          <div class="flex w-4/12 items-center justify-center space-x-2">
            <div class="text-5xl font-semibold">14</div>
            <div>
              <div>March 2022</div>
              <div class="text-sm text-gray-400">Monday</div>
            </div>
          </div>
          <div class="flex w-2/12 justify-center text-3xl">&rarr;</div>
          <div class="flex w-4/12 items-center justify-center space-x-2">
            <div class="text-5xl font-semibold">20</div>
            <div>
              <div>March 2022</div>
              <div class="text-sm text-gray-400">Sunday</div>
            </div>
          </div>
          <div class="flex w-1/12 justify-center">
            <button
              class="rounded-full font-semibold text-primary hover:bg-primary hover:text-gray-200"
            >
              <span
                class="iconify"
                data-height="48"
                data-icon="bx:right-arrow-circle"
                data-width="48"
              ></span>
            </button>
          </div>
        </div>
      </div>

      <div class="flex w-full pt-10">
        <TabGroup as="div" class="flex w-full flex-col">
          <TabList class="flex w-full border-b border-gray-300 text-gray-700">
            <Tab
              v-for="category in categories"
              :key="category"
              v-slot="{ selected }"
              as="template"
            >
              <button
                :class="[
                  'inline-block rounded-t-lg  px-4 py-2',
                  selected
                    ? 'border-b-4 border-blue-500 font-bold dark:text-gray-200'
                    : 'text-gray-500 dark:text-gray-200',
                ]"
              >
                {{ category }}
                <span
                  class="ml-1 rounded-full bg-gray-200 py-1 px-2 text-gray-700 dark:bg-gray-700 dark:text-gray-200"
                >
                  0
                </span>
              </button>
            </Tab>
          </TabList>

          <TabPanels class="mt-2">
            <TabPanel v-for="idx in Object.values(categories)" :key="idx">
              <TimeSheet />
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
import TimeSheet from "@/components/TimeSheet/weekly/Hourly.vue"

const categories = ref(["Hourly employees", "Salaried employees"])
</script>

<style scoped></style>