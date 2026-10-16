# Nuxt 3 SPA - About & Contact Pages Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Thêm 2 trang `/about` và `/contact` cùng thanh điều hướng `<NuxtLink>` cho dự án Nuxt 3 SPA `skinlab-landing`, giữ nguyên giao diện trang chủ ban đầu.

**Architecture:** Cấu hình Nuxt 3 chạy ở chế độ Client-side SPA (`ssr: false`). Sử dụng file-based routing trong thư mục `app/pages/` với `index.vue` (hiển thị `<NuxtWelcome />`), `about.vue`, và `contact.vue`. Tích hợp thanh điều hướng trong `app/app.vue` với `<NuxtPage />`.

**Tech Stack:** Vue 3.5, Nuxt 3.21, Vue Router (tích hợp sẵn trong Nuxt 3).

## Global Constraints

- Chế độ hoạt động: SPA mode (`ssr: false` trong `nuxt.config.ts`).
- Giữ nguyên giao diện trang chủ (`/`) bằng cách sử dụng `<NuxtWelcome />` trong `app/pages/index.vue`.
- Điều hướng hoàn toàn phía client không tải lại trang với `<NuxtLink>`.
- Giao diện đơn giản, phục vụ test code, không dùng thêm thư viện ngoài.

---

### Task 1: Cấu hình SPA Mode trong `nuxt.config.ts`

**Files:**
- Modify: `nuxt.config.ts`

**Interfaces:**
- Produces: `ssr: false` trong Nuxt configuration.

- [ ] **Step 1: Cập nhật `nuxt.config.ts` để kích hoạt SPA mode**

```typescript
// https://nuxt.com/docs/api/configuration/nuxt-config
export default defineNuxtConfig({
  ssr: false,
  compatibilityDate: '2025-07-15',
  devtools: { enabled: true }
})
```

- [ ] **Step 2: Chạy `npx nuxi prepare` để đồng bộ cấu hình**

Run: `npx nuxi prepare`
Expected: `✔ Types generated in .nuxt`

- [ ] **Step 3: Commit cấu hình SPA**

```bash
git add nuxt.config.ts
git commit -m "chore: enable spa mode in nuxt.config.ts"
```

---

### Task 2: Tạo các trang trong `app/pages/`

**Files:**
- Create: `app/pages/index.vue`
- Create: `app/pages/about.vue`
- Create: `app/pages/contact.vue`

**Interfaces:**
- Consumes: `<NuxtWelcome />` từ Nuxt 3.
- Produces: 3 routes `/`, `/about`, `/contact`.

- [ ] **Step 1: Tạo file `app/pages/index.vue` giữ nguyên giao diện hiện tại**

```vue
<template>
  <div>
    <NuxtWelcome />
  </div>
</template>
```

- [ ] **Step 2: Tạo file `app/pages/about.vue`**

```vue
<template>
  <div class="page-container">
    <h1>About SkinLab</h1>
    <p>Chào mừng bạn đến với trang giới thiệu SkinLab demo.</p>
    <p>Đây là trang test SPA routing được xây dựng bằng Vue.js 3 và Nuxt 3.</p>
    <div class="actions">
      <NuxtLink to="/" class="btn">Quay lại Trang Chủ</NuxtLink>
    </div>
  </div>
</template>

<style scoped>
.page-container {
  max-width: 800px;
  margin: 40px auto;
  padding: 24px;
  font-family: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
  color: #1e293b;
}

h1 {
  font-size: 2rem;
  color: #0f172a;
  margin-bottom: 16px;
}

p {
  line-height: 1.6;
  color: #475569;
  margin-bottom: 12px;
}

.actions {
  margin-top: 24px;
}

.btn {
  display: inline-block;
  padding: 10px 20px;
  background-color: #0284c7;
  color: #ffffff;
  text-decoration: none;
  border-radius: 6px;
  font-weight: 500;
  transition: background-color 0.2s ease;
}

.btn:hover {
  background-color: #0369a1;
}
</style>
```

- [ ] **Step 3: Tạo file `app/pages/contact.vue` kèm form test reactivity**

```vue
<script setup>
import { reactive, ref } from 'vue'

const form = reactive({
  name: '',
  email: '',
  message: ''
})

const submitted = ref(false)

function handleSubmit() {
  submitted.value = true
  alert(`Cảm ơn ${form.name || 'bạn'}! Thông tin đã được gửi thành công (Test SPA).`)
  form.name = ''
  form.email = ''
  form.message = ''
}
</script>

<template>
  <div class="page-container">
    <h1>Contact SkinLab</h1>
    <p>Trang liên hệ kiểm tra tính năng form và Vue 3 reactivity trong Nuxt 3 SPA.</p>

    <div v-if="submitted" class="success-banner">
      ✓ Đã gửi thông tin test thành công!
    </div>

    <form @submit.prevent="handleSubmit" class="contact-form">
      <div class="form-group">
        <label for="name">Họ và tên:</label>
        <input id="name" v-model="form.name" type="text" placeholder="Nhập họ tên" required />
      </div>

      <div class="form-group">
        <label for="email">Email:</label>
        <input id="email" v-model="form.email" type="email" placeholder="example@skinlab.vn" required />
      </div>

      <div class="form-group">
        <label for="message">Lời nhắn:</label>
        <textarea id="message" v-model="form.message" rows="4" placeholder="Nội dung cần tư vấn..." required></textarea>
      </div>

      <div class="form-actions">
        <button type="submit" class="btn-submit">Gửi tin nhắn</button>
        <NuxtLink to="/" class="btn-secondary">Quay lại Trang Chủ</NuxtLink>
      </div>
    </form>
  </div>
</template>

<style scoped>
.page-container {
  max-width: 600px;
  margin: 40px auto;
  padding: 24px;
  font-family: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
  color: #1e293b;
}

h1 {
  font-size: 2rem;
  color: #0f172a;
  margin-bottom: 8px;
}

p {
  color: #475569;
  margin-bottom: 24px;
}

.success-banner {
  background-color: #ecfdf5;
  color: #065f46;
  border: 1px solid #a7f3d0;
  padding: 12px 16px;
  border-radius: 6px;
  margin-bottom: 20px;
  font-weight: 500;
}

.contact-form {
  display: flex;
  flex-direction: column;
  gap: 16px;
}

.form-group {
  display: flex;
  flex-direction: column;
  gap: 6px;
}

label {
  font-size: 0.9rem;
  font-weight: 600;
  color: #334155;
}

input, textarea {
  padding: 10px 14px;
  border: 1px solid #cbd5e1;
  border-radius: 6px;
  font-size: 1rem;
  font-family: inherit;
  outline: none;
  transition: border-color 0.2s ease;
}

input:focus, textarea:focus {
  border-color: #0284c7;
}

.form-actions {
  display: flex;
  align-items: center;
  gap: 16px;
  margin-top: 8px;
}

.btn-submit {
  padding: 10px 20px;
  background-color: #0284c7;
  color: #ffffff;
  border: none;
  border-radius: 6px;
  font-size: 1rem;
  font-weight: 500;
  cursor: pointer;
  transition: background-color 0.2s ease;
}

.btn-submit:hover {
  background-color: #0369a1;
}

.btn-secondary {
  text-decoration: none;
  color: #64748b;
  font-size: 0.95rem;
}

.btn-secondary:hover {
  color: #0f172a;
}
</style>
```

- [ ] **Step 4: Chạy `npx nuxi prepare` để nạp các routes mới**

Run: `npx nuxi prepare`
Expected: `✔ Types generated in .nuxt`

- [ ] **Step 5: Commit các pages mới**

```bash
git add app/pages/
git commit -m "feat: add index, about and contact pages"
```

---

### Task 3: Cập nhật `app/app.vue` với Navigation Header & `<NuxtPage />`

**Files:**
- Modify: `app/app.vue`

**Interfaces:**
- Consumes: `<NuxtRouteAnnouncer />`, `<NuxtLink>`, `<NuxtPage />`.
- Produces: Layout giao diện chứa header menu và outlet hiển thị route.

- [ ] **Step 1: Cập nhật `app/app.vue`**

```vue
<template>
  <div class="app-layout">
    <NuxtRouteAnnouncer />
    <header class="app-header">
      <div class="brand">SkinLab</div>
      <nav class="nav-links">
        <NuxtLink to="/" class="nav-item">Home</NuxtLink>
        <NuxtLink to="/about" class="nav-item">About</NuxtLink>
        <NuxtLink to="/contact" class="nav-item">Contact</NuxtLink>
      </nav>
    </header>

    <main class="app-main">
      <NuxtPage />
    </main>
  </div>
</template>

<style>
/* Reset cơ bản cho toàn bộ app */
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
</style>

<style scoped>
.app-layout {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
}

.app-header {
  position: sticky;
  top: 0;
  z-index: 100;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 14px 28px;
  background-color: #ffffff;
  border-bottom: 1px solid #e2e8f0;
  font-family: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.05);
}

.brand {
  font-size: 1.25rem;
  font-weight: 700;
  color: #0f172a;
  letter-spacing: -0.5px;
}

.nav-links {
  display: flex;
  gap: 20px;
}

.nav-item {
  text-decoration: none;
  color: #64748b;
  font-weight: 500;
  font-size: 0.95rem;
  padding: 6px 12px;
  border-radius: 6px;
  transition: all 0.2s ease;
}

.nav-item:hover {
  color: #0284c7;
  background-color: #f0f9ff;
}

.nav-item.router-link-active {
  color: #0284c7;
  font-weight: 600;
  background-color: #e0f2fe;
}

.app-main {
  flex: 1;
}
</style>
```

- [ ] **Step 2: Kiểm tra cú pháp và build thử nghiệm**

Run: `npm run build`
Expected: `✔ You can now preview your build` hoặc build thành công không có lỗi cú pháp.

- [ ] **Step 3: Commit cập nhật `app/app.vue`**

```bash
git add app/app.vue
git commit -m "feat: add top navigation header and NuxtPage outlet"
```

---

### Task 4: Kiểm thử toàn diện (Verification)

**Files:**
- Test check: Toàn bộ project

- [ ] **Step 1: Chạy build production để đảm bảo bundle SPA hoàn toàn hợp lệ**

Run: `npm run build`
Expected: Quá trình build hoàn tất với exit code 0.

- [ ] **Step 2: Kiểm tra các file route đã được sinh ra chính xác**

Run: `git status`
Expected: Working tree clean, các file mới đã được commit.
