<template>
  <div class="max-w-md mx-auto mt-8 p-4">
    <h2 class="text-2xl font-bold mb-6">會員註冊</h2>
    
    <form @submit.prevent="handleSubmit" class="space-y-4">
      <div>
        <label for="account" class="block mb-1">帳號</label>
        <input 
          id="account"
          v-model="form.account"
          data-test="account"
          type="text"
          class="w-full border rounded px-3 py-2"
          required
        >
      </div>

      <div>
        <label for="password" class="block mb-1">密碼</label>
        <input 
          id="password"
          v-model="form.password"
          data-test="password"
          type="password"
          class="w-full border rounded px-3 py-2"
          required
        >
        <p class="text-sm text-gray-500 mt-1">密碼需要包含英文和數字，至少 8 個字元</p>
      </div>

      <div>
        <label for="email" class="block mb-1">Email</label>
        <input 
          id="email"
          v-model="form.email"
          data-test="email"
          type="email"
          class="w-full border rounded px-3 py-2"
          required
        >
      </div>

      <div>
        <label for="phone" class="block mb-1">電話</label>
        <input 
          id="phone"
          v-model="form.phone"
          data-test="phone"
          type="tel"
          class="w-full border rounded px-3 py-2"
          required
        >
      </div>

      <div v-if="error" data-test="error" class="text-red-500">
        {{ error }}
      </div>

      <div v-if="message" data-test="message" class="text-green-500">
        {{ message }}
      </div>

      <button 
        type="submit"
        data-test="submit"
        class="w-full bg-blue-500 text-white py-2 px-4 rounded hover:bg-blue-600"
      >
        註冊
      </button>
    </form>
  </div>
</template>

<script setup>
import { reactive, ref } from 'vue'

const form = reactive({
  account: '',
  password: '',
  email: '',
  phone: ''
})

const error = ref('')
const message = ref('')

const handleSubmit = () => {
  if (form.account === "") {
    error.value = "帳號未填寫"
    return 
  }

  if (form.password === ""){
    error.value = "密碼未填寫"
    return
  } 

  if (form.password.length < 8) {
    error.value = "密碼長度需超過 8 位數"
    return
  }
  
  if (!/^(?=.*[a-zA-Z])(?=.*[0-9]).+$/.test(form.password)) {
    error.value = '密碼須包含英文和數字'
    return
  }

  if (form.email === ""){
    error.value = "信箱未填寫"
    return 
  }

  if (form.phone === ""){
    error.value = "手機未填寫"
    return
  }

  message.value = "註冊成功"  
  return
}
</script>