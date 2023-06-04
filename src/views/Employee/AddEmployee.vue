<template>
  <div class="flex h-auto w-full flex-col justify-center space-y-4">

    <div
      class="flex h-full w-full max-w-5xl flex-col self-center rounded bg-white py-4 px-10 pb-16 shadow dark:bg-primary-gray-dark">
      <!-- Personal Information -->
      <div class="pb-4 text-2xl font-normal text-gray-800 dark:text-gray-200">
        Personal Information
      </div>
      <!-- Personal Information Form -->
      <div class="w-full text-gray-500 dark:text-gray-200">
        <div class="rounded border border-gray-400 p-6 px-24">
          <div class="flex w-full space-x-2 py-2">
            <div class="w-4/12 text-right">
              <label for="Name" class="text-sm font-semibold">Name<span class="color-red p-1">*</span></label>
            </div>
            <div class="flex w-8/12 flex-col space-y-2">
              <input type="text" name="firstName" placeholder="First Name" v-model="empl.name"
                class="rounded border border-gray-300 p-2"
                :class="{ 'border-red-200': $isEmpty(empl.name && empl.surname) }" required />
              <input type="text" name="lastName" placeholder="Last Name" v-model="empl.surname"
                :class="{ 'border-red-200': $isEmpty(empl.name && empl.surname) }"
                class="rounded border border-gray-300 p-2" />
            </div>
          </div>
          <div class="flex justify-center space-x-2 py-2">
            <div class="flex w-4/12 justify-end">
              <label for="addressLine1" class="text-sm font-semibold">Home Address<span
                  class="color-red p-1">*</span></label>
            </div>
            <div class="flex w-8/12 flex-col">
              <div class="w-full">
                <input type="text" name="addressLine1" placeholder="Street" v-model="empl.address.street"
                  class="w-full rounded-t border border-gray-300 p-2"
                  :class="{ 'border-red-200': $isEmpty(empl.address.street) }" />
              </div>
              <div class="flex w-full">
                <input type="text" name="city" v-model="empl.address.city" placeholder="City"
                  :class="{ 'border-red-200': $isEmpty(empl.address.city) }"
                  class="w-full rounded-bl border border-gray-300 p-2" />
                <select class="w-full border border-gray-300 p-2" name="city" id="city" v-model="empl.address.country"
                  :class="{ 'border-red-200': $isEmpty(empl.address.country) }">
                  <option v-for="(province, index) in provinces" :key="index" :value="province.label">
                    {{ province.label }}
                  </option>
                </select>
                <input type="text" name="postalCode" placeholder="Postal Code" v-model="empl.code"
                  :class="{ 'border-red-200': $isEmpty(empl.code) }" id="code"
                  class="w-full rounded-br border border-gray-300 p-2" />
              </div>
            </div>
          </div>
          <!-- <div class="flex items-center space-x-2 py-2">
            <div class="w-4/12 text-right"></div>
            <div class="flex w-8/12 items-center space-x-2">
              <input type="checkbox" name="employeeInvitation" v-model="inviteEmployee" />
              <label for="firstName" class="text-sm">Invite Employee to onboard and enter information</label>
            </div>
          </div> -->
          <div class="flex items-center space-x-2 py-2">
            <div class="flex w-4/12 justify-end">
              <label for="firstName" class="text-sm font-semibold">Email<span class="color-red p-1">*</span></label>
            </div>
            <div class="flex w-8/12 flex-col space-y-2">
              <input type="text" name="email" v-model="empl.email" placeholder="johndoe@email.com"
                :class="{ 'border-red-200': $isEmpty(empl.email) }" class="rounded border border-gray-300 p-2"
                id="email" />
              <span v-if="noemail">Email format is incorrect</span>
            </div>
          </div>
        </div>
      </div>

    

      <div class="mt-6 pb-4 text-2xl font-normal text-gray-800 dark:text-gray-200">
        Personal Identification Numbers
      </div>
      <!-- Work Information Form -->
      <div class="w-full text-gray-500 dark:text-gray-200">
        <div class="rounded border border-gray-400 p-6 px-24">

          <div class="flex w-full space-x-2 py-2">
        <div class="w-4/12 text-right">
          <VLabel class="text-sm font-semibold" for="TaxRegistration">Tax Registratoin<span class="color-red p-1">*</span></VLabel>
        </div>
        <div class="flex w-8/12 flex-col space-y-2">
          <input v-model="empl.TaxRegistration"
            class="rounded border border-gray-300 p-2 mb-4 rounded border py-1 px-3 text-slate-900 outline-none transition focus:ring"
            name="TaxRegistration" id="TaxRegistration" type="text" placeholder="Tax Registratoin" />
        </div>
      </div>
          <div class="flex w-full space-x-2 py-2">
            <div class="w-4/12 text-right">
              <VLabel class="text-sm font-semibold" for="NISNumber">NIS Number<span class="color-red p-1">*</span></VLabel>
            </div>
            <div class="flex w-8/12 flex-col space-y-2">
              <input v-model="empl.NISNumber"
                class="rounded border border-gray-300 p-2 mb-4 rounded border py-1 px-3 text-slate-900 outline-none transition focus:ring"
                name="NISNumber" id="NISNumber" type="text" placeholder="NIS Number" />
            </div>
          </div>
        </div>
      </div>



      <!-- Work Information -->
      <div class="mt-6 pb-4 text-2xl font-normal text-gray-800 dark:text-gray-200">
        Work Information
      </div>
      <!-- Work Information Form -->
      <div class="w-full text-gray-500 dark:text-gray-200">
        <div class="rounded border border-gray-400 p-6 px-24">
          <div class="flex items-center space-x-2 py-2">
            <div class="flex w-4/12 justify-end">
              <label for="date_of_hire" class="text-sm font-semibold">Date of Hire<span
                  class="color-red p-1">*</span></label>
            </div>
            <div class="flex w-5/12 flex-col space-y-2">
              <input type="date" name="date_of_hire" v-model="empl.date_of_hire"
                class="rounded border border-gray-300 p-2" />
            </div>
          </div>
          <div class="flex items-center space-x-2 py-2">
            <div class="flex w-4/12 justify-end">
              <label for="WorkLocation" class="text-sm font-semibold">Work Location<span
                  class="color-red p-1">*</span></label>
            </div>
            <div class="flex w-8/12 flex-col space-y-2">
              <select v-if="selectMode" class="w-full  rounded border border-gray-300 p-2" name="WorkLocation"
                v-model="empl.WorkLocation" id="WorkLocation">
                <option value="Home">Work From Home</option>
                <option value="Office">Head Office </option>
              </select>
              <!-- <input v-else type="text" name="WorkLocation" 
                v-model="empl.WorkLocation" 
                placeholder="Work From Home"
                class="w-10/12 rounded border border-gray-300 p-2" />
                <button v-if="selectMode" @click="selectMode=!selectMode,empl.WorkLocation=''"
                class="w-2/12 p-2 border border-gray-200"
                >Input</button>
                <button v-else @click="selectMode=!selectMode,empl.WorkLocation=''"
                class="w-2/12 p-2 border border-gray-200"
                >Select</button> -->
            </div>
          </div>
          <div class="flex items-center space-x-2 py-2">
            <div class="flex w-4/12 justify-end">
              <label for="SalaryType" class="text-sm font-semibold">Salary Type<span
                  class="color-red p-1">*</span></label>
            </div>
            <div class="flex w-8/12 flex-col space-y-2">
              <select class="w-full rounded border border-gray-300 p-2" name="SalaryType" v-model="empl.SalaryType"
                id="SalaryType">
                <option value="hourly">Per hour</option>
                <option value="annual">Per year</option>
              </select>
            </div>
          </div>
          <div class="flex items-center space-x-2 py-2">
            <div class="flex w-4/12 justify-end">
              <label for="SalaryAmount" class="text-sm font-semibold">Salary Amount<span
                  class="color-red p-1">*</span></label>
            </div>
            <div class="flex  flex-col space-y-2">
              <div class="input-wrapper">
                <span class="money-sign">$</span>
                <input type="number" v-model="empl.SalaryAmount" name="SalaryAmount" class="rounded    p-2"
                  :class="{ 'border-red-200': $isEmpty(empl.SalaryAmount) }" />
              </div>
            </div>
          </div>
          <div class="flex space-x-2 py-2">
            <div class="flex w-4/12 justify-end">
              <label for="DirectDeposit" class="text-sm font-semibold">Direct Deposit<span
                  class="color-red p-1">*</span></label>
            </div>

            <div class="flex flex-col space-y-2">
              <div class="flex flex-col">
                <div>
                  <input type="radio" name="DirectDeposit" v-model="empl.DirectDeposit" value="Yes" />
                  <label for="DirectDeposit" class="ml-2 text-sm text-gray-600 dark:text-gray-200">Yes</label>
                  <div class="my-1 max-w-sm rounded bg-yellow-200 px-1 py-1 text-xs text-gray-700">
                    This requires employee bank information.<br /> You can change it
                    anytime.
                  </div>

                </div>
                <div>
                  <input type="radio" name="DirectDeposit" v-model="empl.DirectDeposit" value="No" />
                  <label for="DirectDeposit" class="ml-2 text-sm text-gray-600 dark:text-gray-200">No</label>
                </div>
              </div>
            </div>
          </div>



          <div class="flex items-center space-x-2 py-2">
            <div class="flex w-4/12 justify-end">
              <label for="Vacation" class="text-sm font-semibold">Vacation Policy<span
                  class="color-red p-1">*</span></label>
            </div>
            <div class="flex w-8/12 flex-col space-y-2">
              <select class="w-full rounded border border-gray-300 p-2" name="Vacation" id="Vacation"
                v-model="empl.Vacation">
                <option value="offer">Don't offer vacation time for this employee
                </option>
                <option value="Accure">Accure vacation time for this employee</option>
              </select>
            </div>
          </div>
          <div class="flex space-x-2 py-2">
            <div class="flex w-4/12 justify-end">
              <label for="Vacation_rate" class="text-sm font-semibold">Vacation accrual rate<span
                  class="color-red p-1">*</span></label>
            </div>
            <div class="flex w-4/12 flex-col space-y-2">
              <div class="input-wrapper">
                <input type="number" name="Vacation_rate" id="Vacation_rate" class=" p-2" v-model="empl.Vacation_rate"
                  :class="{ 'border-red-200': $isEmpty(empl.SalaryAmount) }" /><span class="percent-sign">%</span>
              </div>
              <span class="text-xs text-gray-600 dark:text-gray-200">
                e.g. 4.0% of regular hours on a 40 hour/week payroll period
                translates to 80 hours/week</span>
            </div>
          </div>
          <div class="flex items-center space-x-2 py-2">
            <div class="w-4/12 text-right"></div>
            <div class="flex w-8/12 items-center space-x-2">
              <button class="rounded bg-primary px-2 py-2 text-white transition hover:bg-primary-dark"
                @click="validateInput">
                Save Employee
              </button>

              <router-link :to="{ name: 'employees' }"
                class="rounded border border-primary px-2 py-2 transition hover:bg-primary hover:text-gray-100">
                Discard Changes
              </router-link>
            </div>
          </div>
        </div>
      </div>
    </div>
    <Modal :visible="isModalview" @ok="closeModal" class="text-center w-full " width="750px" :footer="false"
      :closable="false">
      <div class="svg-box">
        <svg class="circular green-stroke">
          <circle class="path" cx="75" cy="75" r="50" fill="none" stroke-width="5" stroke-miterlimit="10" />
        </svg>
        <svg class="checkmark green-stroke">
          <g transform="matrix(0.79961,8.65821e-32,8.39584e-32,0.79961,-489.57,-205.679)">
            <path class="checkmark__check" fill="none" d="M616.306,283.025L634.087,300.805L673.361,261.53" />
          </g>
        </svg>
      </div>
      <h1>Your employee has been added</h1>
      <h3>You're ready to <span>add more details about this employee</span> like tax and direct deposit information.
      </h3>
      <h4>We have also invited this employee to Wave to help you complete their profile and view paystubs.</h4>
      <button class="text-bold rounded-full border border-sky-500 p-2 mt-7 mr-4" @click="close" aria-label="Close modal">
        <router-link :to="{ name: 'add-employee' }">
          Add another
        </router-link>
      </button>
      <button class="rounded-full border border-sky-500 p-2 bg-blue-500 text-white" @click="close"
        aria-label="Close modal">
        <router-link :to="{ name: 'edit-employee', params: { id: userid } }">
          <div class="text-white">Done adding employees</div>
        </router-link>
      </button>
    </Modal>
  </div>
</template>
<script setup lang="ts">
import { ref } from "vue"
const baseApiURL = import.meta.env.VITE_API_BASE_URL
const urlforSave = `${baseApiURL}/employee/add`
import { Modal, Button, notification } from 'ant-design-vue'
function close() {
  isModalview.value = false
}
const currentDate = new Date();
const year = currentDate.getFullYear();
const month = String(currentDate.getMonth() + 1).padStart(2, "0"); // Note that month is zero-indexed
const day = String(currentDate.getDate()).padStart(2, "0");
const formattedDateTime = `${year}-${month}-${day}`;
const empl = ref({
  name: "",
  surname: "",
  code: '',
  email: "",
  TaxRegistration: "",
  NISNumber: "",
  address: {
    street: "",
    country: "",
    city: ""
  },
  date_of_hire: '',
  WorkLocation: 'Office',
  SalaryType: 'hourly',
  SalaryAmount: '',
  DirectDeposit: 'Yes',
  Vacation: 'offer',
  Vacation_rate: '',
  Status: 'active'
})
function formartvalue() {
  empl.value.name = ''
  empl.value.surname = ''
  empl.value.code = ''
  empl.value.email = ''
  empl.value.TaxRegistration=""
  empl.value.NISNumber= ""
  empl.value.date_of_hire = formattedDateTime
  empl.value.address.street = ''
  empl.value.address.country = ''
  empl.value.address.city = ''
  empl.value.WorkLocation = 'Office',
    empl.value.SalaryType = 'hourly',
    empl.value.SalaryAmount = '',
    empl.value.DirectDeposit = 'Yes',
    empl.value.Vacation = 'offer',
    empl.value.Vacation_rate = '',
    empl.value.Status = 'active'
}
onMounted(() => {
  empl.value.date_of_hire = formattedDateTime
})
const isModalview = ref(false)
const userid = ref('')
const noemail = ref(false)
const selectMode = ref(true)
function emailcheck() {
  let regex = /\S+@\S+\.\S+/;
  console.log(regex.test(empl.value.email))
  if (regex.test(empl.value.email)) {
    noemail.value = false
  } else {
    noemail.value = true
  }
}
async function validateInput() {
  await emailcheck()
  if (empl.value.name === '' || empl.value.surname == '' || empl.value.email === '' || empl.value.code === '' || empl.value.SalaryAmount === '' || empl.value.Vacation_rate === '' || empl.value.TaxRegistration === '' || empl.value.NISNumber === '') {
    notification.error({
      message: 'Warning',
      description: 'There is a field that has not been entered.'
    })
  } else if (noemail.value === true) {
    // alert('Email format is incorrect')
    notification.error({
      message: 'Warning',
      description: 'Email format is incorrect.'
    })
    document.getElementById('email')?.focus()

  } else {
    const checks = `${baseApiURL}/employee/check`
    const response = await fetch(checks, {
      method: "POST",
      body: JSON.stringify({
        email: empl.value.email,
        TaxRegistration: empl.value.TaxRegistration,
        NISNumber: empl.value.NISNumber
      }),
      headers: {
        "Content-Type": "application/json",
      },
    }).then((r) => r.json())
    const { isSuccessful, emailallow, TaxRegistrationallow, NISNumberallow } = response
    if (isSuccessful) {
      if (!emailallow) {
        notification.warning({
          message: 'Warning',
          description: 'Email  ready used.'
        })
        document.getElementById('email')?.focus()
      } else if (!TaxRegistrationallow && !NISNumberallow) {
        // alert('email and code ready used')
        notification.warning({
          message: 'Warning',
          description: 'Tax and NISN ready used.'
        })
        document.getElementById('TaxRegistration')?.focus()
      } else if (!TaxRegistrationallow) {
        // alert('code ready used')
        notification.warning({
          message: 'Warning',
          description: 'Tax Registration ready used.'
        })
        document.getElementById('TaxRegistration')?.focus()
      } else if (!NISNumberallow) {
        // alert('email  ready used')
        notification.warning({
          message: 'Warning',
          description: 'NIS Number  ready used.'
        })
        document.getElementById('NISNumber')?.focus()
      } else {
        SaveEmployee()
      }
    } else {
      notification.warning({
        message: 'Error',
        description: 'Server connect has failed.'
      })
    }
  }
}

function closeModal() {
  isModalview.value = false
}
async function SaveEmployee() {
  console.log(empl.value);
  const response = await fetch(urlforSave, {
    method: "POST",
    body: JSON.stringify({
      infodata: empl.value
    }),
    headers: {
      "Content-Type": "application/json",
    },
  }).then((r) => r.json()).catch(() => {
    notification.warning({
      message: 'Error',
      description: 'Error occurred on server.'
    })
  })
  console.log(response);
  if (response.isSuccessful) {
    userid.value = response.CreateEmployee.id
    isModalview.value = true
    formartvalue()

  } else {
    notification.warning({
      message: 'Error',
      description: 'Operation failed..'
    })
  }
}
const provinces = [
  {
    name: "Alberta",
    label: "AB",
  },
  {
    name: "British Columbia",
    label: "BC",
  },
  {
    name: "Manitoba",
    label: "MB",
  },
  {
    name: "New Brunswick",
    label: "NB",
  },
  {
    name: "Newfoundland and Labrador",
    label: "NL",
  },
  {
    name: "Northwest Territories",
    label: "NT",
  },
  {
    name: "Nova Scotia",
    label: "NS",
  },
  {
    name: "Nunavut",
    label: "NU",
  },
  {
    name: "Ontario",
    label: "ON",
  },
  {
    name: "Prince Edward Island",
    label: "PE",
  },
  {
    name: "Quebec",
    label: "QC",
  },
  {
    name: "Saskatchewan",
    label: "SK",
  },
  {
    name: "Yukon",
    label: "YT",
  },
]
</script>
<style scoped>
.error {
  border: red solid 1px;
}

.color-red {
  color: red
}

.input-wrapper1 {
  border-width: 1px;
  border-style: solid;
  padding: -10px;
  margin: 0px
}

.input-wrapper {
  border-width: 1px;
  border-style: solid;
  padding-left: 0px;
}

.percent-sign {
  margin-left: 10px
}

.money-sign {
  margin-right: 10px;
  margin-left: 10px;
}

h1 {
  font-size: 250%;
  font-family: 'Century Gothic';
}

h3 {
  font-family: 'Century Gothic';
  color: #444444;
}

span {
  color: rgb(54, 90, 209);
  font-weight: bolder;
}

h4 {
  font-family: 'Century Gothic';
  color: #666666;
}


.btn-add {
  color: rgb(241, 241, 241);
}

.btn-add:hover {
  animation: 0.5s fromWhitetoBlue ease-out;
  background-color: rgb(87, 112, 194);
  color: white;
}

@keyframes fromWhitetoBlue {
  0% {
    background-color: white;
    color: rgb(34, 60, 148);
  }

  80% {
    background-color: rgb(54, 90, 209);
    color: white;
  }

  100% {
    background-color: rgb(87, 112, 194);
    color: white;
  }
}

.btn-done {
  color: white;
  background-color: rgb(54, 90, 209);
}

.btn-done:hover {
  animation: 0.5s fromBluetoWhite ease-out;
  color: rgb(34, 60, 148);
  background-color: rgba(54, 90, 209, 0.253);
}

@keyframes fromBluetoWhite {
  0% {
    color: white;
    background-color: rgb(54, 90, 209);
  }

  80% {
    color: rgb(34, 60, 148);
    background-color: white;
  }

  100% {
    color: rgb(34, 60, 148);
    background-color: rgba(54, 90, 209, 0.253);
  }
}

.svg-box {
  display: inline-block;
  position: relative;
  width: 150px;
}

.green-stroke {
  stroke: #39b13f;
}


.circular circle.path {
  stroke-dasharray: 380;
  stroke-dashoffset: 0;
  stroke-linecap: round;
  opacity: 0.7;
  animation: 0.7s draw-circle ease-out;
}


/*------- Checkmark ---------*/
.checkmark {
  stroke-width: 6.25;
  stroke-linecap: round;
  position: absolute;
  top: 56px;
  left: 49px;
  width: 52px;
  height: 40px;
}

.checkmark path {
  animation: 1s draw-check ease-out;
}

@keyframes draw-circle {
  0% {
    stroke-dasharray: 0, 330;
    stroke-dashoffset: 0;
    opacity: 1;
  }

  80% {
    stroke-dasharray: 330, 330;
    stroke-dashoffset: 0;
    opacity: 1;
  }

  100% {
    opacity: 0.4;
  }
}

@keyframes draw-check {
  0% {
    stroke-dasharray: 49, 80;
    stroke-dashoffset: 48;
    opacity: 0;
  }

  50% {
    stroke-dasharray: 49, 80;
    stroke-dashoffset: 48;
    opacity: 1;
  }

  100% {
    stroke-dasharray: 130, 80;
    stroke-dashoffset: 48;
  }
}
</style>
