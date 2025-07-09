<script setup>
import { reactive, ref } from 'vue'
import TextInput from './components/Form/TextInput.vue'
import BaseSelect from './components/Form/BaseSelect.vue'
import Label from './components/Form/Label.vue';

const boards = reactive([
  {
    label: "Dinajpur",
    value: "dinajpur",
  },

  {
    label: "Dhaka",
    value: "dhaka",
  }

]);

// Generate year list from 1996 to current year
const currentYear = new Date().getFullYear()
const years = Array.from({ length: currentYear - 1996 + 1 }, (_, i) => currentYear - i)


const form = ref({
  exam: 'SSC',
  year: '',
  board: '',
  roll: '',
  reg: '',
  captcha: '',
})

const result = ref(null)

const captchaUrl = ref(generateCaptchaUrl())

function generateCaptchaUrl() {
  return `https://eboardresults.com/v2/captcha?t=${Date.now()}`
}

function reloadCaptcha() {
  captchaUrl.value = generateCaptchaUrl()
}

function submitForm() {
  // Replace this with your API call logic
  result.value = {
    name: 'Rahim Uddin',
    roll: form.value.roll,
    gpa: '5.00',
    subjects: [
      { name: 'Bangla', grade: 'A+' },
      { name: 'English', grade: 'A+' },
      { name: 'Math', grade: 'A+' },
      { name: 'Physics', grade: 'A+' },
      { name: 'Chemistry', grade: 'A+' },
    ]
  }
}
</script>


<template>
  <div class="min-h-screen bg-gray-900 text-white">
    <!-- Header -->
    <header class="p-4 bg-gray-800 shadow-md">
      <h1 class="text-xl font-semibold text-center">📘 Online Result Checker</h1>
    </header>

    <!-- Result Form Section -->
    <section class="p-4 max-w-md mx-auto space-y-4 ">
      <div>
        <label class="block mb-1 text-sm">Examination</label>
        <BaseSelect v-model="form.board">
          <option selected value="">Select One</option>
          <option v-for="(board, index) in boards" :key="index" :value="board.value" >{{ board.label }}</option>
        </BaseSelect>
      </div>

      <div>
        <label class="block mb-1 text-sm">Year</label>

        <BaseSelect v-model="form.year">
          <option value="" disabled selected>Select One</option>
          <option v-for="(year, index) in years" :key="index" :value="year">
            {{ year }}
          </option>

        </BaseSelect>




      </div>

      <div>
        <label class="block mb-1 text-sm">Board</label>
        <select v-model="form.board" class="w-full bg-gray-800 text-white border border-gray-600 rounded p-2">

          <option value="">Select One</option>
          <option value="jsc">JSC/JDC</option>
          <option value="ssc">SSC/Dakhil/Equivalent</option>
          <option value="hsc">HSC/Alim/Equivalent</option>

        </select>
      </div>

      <div>
        <label class="block mb-1 text-sm">Roll</label>
        <input v-model="form.roll" type="text"
          class="w-full bg-gray-800 text-white border border-gray-600 rounded p-2" />
      </div>

      <div>
        <label class="block mb-1 text-sm">Reg No</label>
        <input v-model="form.reg" type="text"
          class="w-full bg-gray-800 text-white border border-gray-600 rounded p-2" />
      </div>

      <div>
        <label class="block mb-1 text-sm">CAPTCHA</label>
        <div class="flex items-center gap-2">
          <img :src="captchaUrl" @click="reloadCaptcha" class="w-28 h-10 border cursor-pointer"
            title="change captcha code" />
          <input v-model="form.captcha" type="text"
            class="flex-1 bg-gray-800 text-white border border-gray-600 rounded p-2" placeholder="captcha code" />
        </div>
      </div>

      <button @click="submitForm" class="w-full bg-pink-600 hover:bg-pink-700 rounded p-2 text-white font-semibold">
        Check Result
      </button>
    </section>

    <!-- Result Section -->
    <section v-if="result" class="p-4 max-w-md mx-auto space-y-4">
      <div class="bg-gray-800 rounded-lg p-4 shadow">
        <h2 class="text-lg font-bold mb-2">🎓 {{ result.name }}</h2>
        <p><strong>Roll:</strong> {{ result.roll }}</p>
        <p><strong>GPA:</strong> {{ result.gpa }}</p>
      </div>

      <div class="overflow-x-auto">
        <table class="w-full text-sm text-left border border-gray-700">
          <thead class="bg-gray-700">
            <tr>
              <th class="p-2 border border-gray-600">Subject</th>
              <th class="p-2 border border-gray-600">Grade</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="subject in result.subjects" :key="subject.name" class="hover:bg-gray-800">
              <td class="p-2 border border-gray-700">{{ subject.name }}</td>
              <td class="p-2 border border-gray-700">{{ subject.grade }}</td>
            </tr>
          </tbody>
        </table>
      </div>
    </section>

    <!-- Footer -->
    <footer class="p-4 text-center text-sm text-gray-500 mt-10">
      &copy; {{ new Date().getFullYear() }} | Developed by <a href="" class="text-gray-300">Sarjid Islam Habil</a>
    </footer>
  </div>
</template>
