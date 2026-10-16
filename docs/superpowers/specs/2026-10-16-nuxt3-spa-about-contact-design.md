# Design Spec: Nuxt 3 SPA - Add /about and /contact Pages

## 1. Overview
Triển khai thêm 2 trang `/about` và `/contact` cho dự án Vue.js / Nuxt 3 (`skinlab-landing`), tuân thủ chuẩn Single Page Application (SPA), phục vụ mục đích kiểm tra code và điều hướng client-side đơn giản.

## 2. Requirements & Constraints
- **Chế độ hoạt động**: Chạy chế độ SPA hoàn toàn (`ssr: false`).
- **Trang chủ (`/`)**: Giữ nguyên 100% giao diện mặc định hiện tại của Nuxt (`<NuxtWelcome />`).
- **Điều hướng**: Sử dụng thẻ `<NuxtLink>` của Nuxt 3 để chuyển trang mượt mà không reload trang.
- **Trang `/about`**: Giao diện đơn giản hiển thị thông tin giới thiệu và liên kết điều hướng.
- **Trang `/contact`**: Giao diện đơn giản gồm form liên hệ cơ bản (Họ tên, Email, Lời nhắn) có xử lý sự kiện submit (reactive state) để test tính năng trong môi trường SPA.

## 3. Architecture & File Structure

```text
skinlab-landing/
├── nuxt.config.ts        # Thêm `ssr: false`
├── app/
│   ├── app.vue           # Header điều hướng tối giản + <NuxtPage />
│   └── pages/
│       ├── index.vue     # Trang Home hiển thị <NuxtWelcome />
│       ├── about.vue     # Trang About đơn giản
│       └── contact.vue   # Trang Contact đơn giản với form test
```

## 4. Implementation Details

### 4.1. `nuxt.config.ts`
- Cấu hình thuộc tính `ssr: false` trong `defineNuxtConfig`.

### 4.2. `app/app.vue`
- Giữ thẻ `<NuxtRouteAnnouncer />`.
- Thêm thanh điều hướng header đơn giản với các liên kết:
  - `Home`: `<NuxtLink to="/">`
  - `About`: `<NuxtLink to="/about">`
  - `Contact`: `<NuxtLink to="/contact">`
- Thêm `<NuxtPage />` để render component tương ứng với route hiện tại.

### 4.3. `app/pages/index.vue`
- Template chứa `<NuxtWelcome />` để bảo toàn nguyên vẹn giao diện khởi tạo ban đầu.

### 4.4. `app/pages/about.vue`
- Cung cấp tiêu đề trang "About SkinLab".
- Nội dung giới thiệu văn bản đơn giản.
- Liên kết `<NuxtLink to="/">` để quay về trang chủ.

### 4.5. `app/pages/contact.vue`
- Cung cấp tiêu đề trang "Contact Us".
- Form nhập liệu: Tên (`name`), Email (`email`), Lời nhắn (`message`).
- Xử lý submit bằng hàm `handleSubmit` trong `<script setup>` (hiển thị thông báo gửi thành công và reset form).
- Liên kết điều hướng về trang chủ.

## 5. Verification
- Chạy lệnh build hoặc dev để kiểm tra router Nuxt 3 nhận diện đúng 3 route: `/`, `/about`, `/contact`.
- Kiểm tra tính năng SPA (click menu không gây reload trình duyệt).
