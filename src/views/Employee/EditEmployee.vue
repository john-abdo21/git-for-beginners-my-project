<template>
  <div v-if="hasEmployee" class="flex h-full w-full justify-center">
    <div
      class="flex h-full w-full max-w-5xl flex-col self-center overflow-y-scroll rounded bg-white py-4 px-10 pb-16 shadow dark:bg-primary-gray-dark"
    >
      <!-- Header -->
      <div class="mb-8 flex justify-between">
        <div
          class="pb-2 text-2xl font-semibold capitalize text-gray-800 dark:text-gray-200"
        >
          {{ userData.name}} {{ userData.surname }}
        </div>
        <router-link
          :to="{ name: 'employees' }"
          class="rounded bg-primary p-2 text-base text-white shadow transition hover:bg-primary-dark"
        >
          Cancel Invite
        </router-link>
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
            <TabPanel key="Personal Information" class="h-full">
              <PersonalInformation :employee="userData" />
            </TabPanel>
            <TabPanel key="Work Information" class="h-full">
              <WorkInformation :employeeId="emplId" />
            </TabPanel>
            <TabPanel key="Compensation" class="h-full">
              <Compensation :employeeId="emplId" />
            </TabPanel>
            <TabPanel key="Vacation" class="h-full">
              <Vacation :employeeId="emplId"/>
            </TabPanel>
            <TabPanel key="Holiday" class="h-full">
              <Holiday :employeeId="emplId"/>
            </TabPanel>
            <TabPanel key="Sick Leaves" class="h-full">
              <SickLeave :employeeId="emplId"/>
            </TabPanel>
            <TabPanel key="Tax Details" class="h-full">
              <TaxDetails :employeeId="emplId"/>
            </TabPanel>
            <TabPanel key="Benefits & Deductions" class="h-full">
              <BenefitsAndDeductions :employeeId="emplId"/>
            </TabPanel>
            <TabPanel key="Employee Files" class="h-full">
              <EmployeeFiles :employeeId="emplId"/>
            </TabPanel>
            <TabPanel key="Emergency Contacts" class="h-full">
              <EmergencyContact :employeeId="emplId"/>
            </TabPanel>
            <TabPanel key="Direct Deposit" class="h-full">
              <DirectDeposit :employeeId="emplId" />
            </TabPanel>
            <TabPanel key="Bank Details" class="h-full">
              <BankDetails :employeeId="emplId"/>
            </TabPanel>
            <TabPanel key="Employment Status" class="h-full">
              <EmploymentStatus :employeeId="emplId"/>
            </TabPanel>
          </TabPanels>
        </TabGroup>
      </div>
    </div>
  </div>
  <div v-else>Employee not selected</div>
</template>

<script lang="ts" setup>
import { onMounted, ref, watch } from "vue"
import { useRoute } from "vue-router"
import { TabGroup, TabList, Tab, TabPanels, TabPanel } from "@headlessui/vue"
import PersonalInformation from "../../components/Employees/EditEmployee/PersonalInformation.vue"
import Compensation from "../../components/Employees/EditEmployee/Compensation.vue"
import WorkInformation from "../../components/Employees/EditEmployee/WorkInformation.vue"

const route = useRoute()

const hasEmployee = ref(false)
const baseApiURL = import.meta.env.VITE_API_BASE_URL
const employeeId =
  Number(route.params.id) > 0 && !Number.isNaN(route.params.id)
    ? route.params.id
    : false
console.log("employeeId: ", employeeId)
const url = `${baseApiURL}/employee/${employeeId}`
const userData = ref(null)
const emplId = ref('')

onMounted(async () => {
  const { employee } = await fetch(url).then((r) => r.json())
  if (employee) {
    userData.value = employee
    emplId.value=employee.id
    hasEmployee.value = true //
  }
})
const categories = ref([
  {
    label: "Personal Information",
    hasErrors: false,
  },
  {
    label: "Work Information",
    hasErrors: false,
  },
  {
    label: "Compensation",
    hasErrors: false,
  },
  {
    label: "Vacation",
    hasErrors: false,
  },
  {
    label: "Holiday",
    hasErrors: false,
  },
  {
    label: "Sick Leaves",
    hasErrors: false,
  },
  {
    label: "Tax Details",
    hasErrors: false,
  },
  {
    label: "Benefits & Deductions",
    hasErrors: false,
  },
  {
    label: "Employee Files",
    hasErrors: false,
  },
  {
    label: "Emergency Contact",
    hasErrors: false,
  },
  {
    label: "Direct Deposit",
    hasErrors: true,
  },
  {
    label: "Bank Details",
    hasErrors: false,
  },
  {
    label: "Employment Status",
    hasErrors: false,
  },
])
</script>
<style scoped></style>