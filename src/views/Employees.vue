<template>
  <div class="flex w-full flex-col rounded bg-white px-2 py-4 shadow dark:bg-primary-gray-dark">
    <!-- Header -->
    <div class="flex justify-between">
      <form action="">
        <div class="group relative">
          <input v-model="search" :class="searchClicked ? 'w-60 bg-gray-100' : 'w-40 bg-gray-50'"
            class="block appearance-none rounded py-2 px-4 pl-2 leading-tight text-gray-700 outline-none transition-all duration-300 ease-in-out"
            placeholder="Search" @blur="searchClicked = false" @focus="searchClicked = true" />
          <div class="absolute inset-y-0 right-0 mr-2 flex items-center pl-3">
            <svg class="h-5 w-5 fill-current text-gray-700 transition-all group-hover:text-primary" name="search"
              viewBox="0 0 24 24">
              <path
                d="M16.32 14.9l1.1 1.1c.4-.02.83.13 1.14.44l3 3a1.5 1.5 0 0 1-2.12 2.12l-3-3a1.5 1.5 0 0 1-.44-1.14l-1.1-1.1a8 8 0 1 1 1.41-1.41l.01-.01zM10 16a6 6 0 1 0 0-12 6 6 0 0 0 0 12z">
              </path>
            </svg>
          </div>
        </div>
      </form>
      <div>
        <router-link :to="{ name: 'add-employee' }"
          class="rounded bg-primary p-2 text-base text-white shadow transition hover:bg-primary-dark">
          Add an Employee
        </router-link>
      </div>
    </div>
    <!-- Body -->
    <div class="flex w-full pt-10">
      <TabGroup as="div" class="flex w-full flex-col">
        <TabList class="flex w-full border-b border-gray-300 text-gray-700">
          <Tab v-for="category in categories" :key="category" v-slot="{ selected }" as="template">
            <button :class="[
              'inline-block rounded-t-lg  px-4 py-2',
              selected
                ? 'border-b-4 border-blue-500 font-bold dark:text-gray-200'
                : 'text-gray-500 dark:text-gray-200',
            ]" >
              {{ category }}
              <span class="ml-1 rounded-full bg-gray-200 py-1 px-2 text-gray-700 dark:bg-gray-700 dark:text-gray-200">
                {{Members[category] }}
              </span>
            </button>
          </Tab>
        </TabList>

        <TabPanels class="mt-2">
          <TabPanel >
            <EmployeeList :employees="activeemployees" />
          </TabPanel>
          <TabPanel >
            <EmployeeList :employees="leaveemployees" />
          </TabPanel>
          <TabPanel >
            <EmployeeList :employees="dismissedemployees" />
          </TabPanel>
        </TabPanels>
      </TabGroup>
    </div>
  </div>
</template>
<script lang="ts" setup>
import { onMounted, ref, computed } from "vue"
import { TabGroup, TabList, Tab, TabPanels, TabPanel } from "@headlessui/vue"
import EmployeeList from "../components/Employees/EmployeeList.vue"

const categories = ref(["active", "OnLeave", "Dismissed"])
const isOpen = ref<boolean>(false)
const search = ref<string>("")
const searchClicked = ref<boolean>(false)
const Members = ref<any>({
  active:0,
  OnLeave:0,
  Dismissed:0
})

const employees = ref<any>([])
const activeemployees = ref<any>([])
const leaveemployees = ref<any>([])
const dismissedemployees = ref<any>([])
onMounted(async () => {
  const allemployeesData = await fetch(`http://localhost:3010/wagez/employees/`).then(
    (r) => r.json()
  )
  employees.value=allemployeesData
  activeemployees.value = allemployeesData.filter((empl: any) => {return empl.Status === 'active'||empl.Status === null})
  leaveemployees.value = allemployeesData.filter((empl: any) => empl.Status === 'leave')
  dismissedemployees.value = allemployeesData.filter((empl: any) => empl.Status === 'boarding')
  Members.value['active']=activeemployees.value.length
  Members.value['OnLeave']=leaveemployees.value.length
  Members.value['Dismissed']=dismissedemployees.value.length
  watch(allemployees, (allemployeesData) => {
  activeemployees.value = allemployeesData.filter((empl: any) => {return empl.Status === 'active'||empl.Status === null})
  leaveemployees.value = allemployeesData.filter((empl: any) => empl.Status === 'leave')
  dismissedemployees.value = allemployeesData.filter((empl: any) => empl.Status === 'boarding')
  Members.value['active']=activeemployees.value.length
  Members.value['OnLeave']=leaveemployees.value.length
  Members.value['Dismissed']=dismissedemployees.value.length

  })
})
const allemployees = computed(() =>
  employees.value.filter((employee: any) => {
    if (search.value.length >=2) {
      return (
        employee.name.toLocaleLowerCase().includes(search.value.toLocaleLowerCase()) ||
        employee.surname.toLocaleLowerCase().includes(search.value.toLocaleLowerCase())
      )
    } else {
      return true
    }
  })
)
</script>