<script setup>
import { ref } from 'vue'

const name = ref('')
const email = ref('')
const message = ref('')
const submitted = ref(false)
const age = ref(Number)(20) 

function handleSubmit() {
  submitted.value = true
  alert(`Gửi thông tin thành công! Tên: ${name.value}, Email: ${email.value}`)
  name.value = ''
  email.value = ''
  message.value = ''
}
</script>

<template>
  <div style="padding: 30px; font-family: sans-serif; max-width: 500px;">
    <h1>Contact SkinLab</h1>
    <p>Trang liên hệ kiểm tra form và Vue reactivity.</p>
    
    <div v-if="submitted" style="margin: 15px 0; padding: 10px; background: #e0f2fe; color: #0369a1; border-radius: 4px;">
      Gửi test thành công!
    </div>

    <form style="display: flex; flex-direction: column; gap: 12px; margin-top: 15px;" @submit.prevent="handleSubmit">
      <div>
        <label style="display: block; margin-bottom: 4px;">Họ và tên:</label>
        <input v-model="name" type="text" placeholder="Nhập tên" required style="width: 100%; padding: 8px; box-sizing: border-box;" >
      </div>

      <div>
        <label style="display: block; margin-bottom: 4px;">Email:</label>
        <input v-model="email" type="email" placeholder="example@skinlab.vn" required style="width: 100%; padding: 8px; box-sizing: border-box;" >
      </div>

      <div>
        <label style="display: block; margin-bottom: 4px;">Nội dung:</label>
        <textarea v-model="message" rows="4" placeholder="Nhập tin nhắn..." required style="width: 100%; padding: 8px; box-sizing: border-box;"/>
      </div>

      <button type="submit" style="padding: 10px; background: #0284c7; color: white; border: none; border-radius: 4px; cursor: pointer;">
        Gửi liên hệ
      </button>
    </form>

    <br >
    <NuxtLink to="/" style="color: #0284c7; text-decoration: underline;">&larr; Quay lại Home</NuxtLink>
  </div>
</template>
