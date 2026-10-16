<template>
  <div>
    <NuxtRouteAnnouncer />
    <nav style="display: flex; gap: 20px; padding: 15px 30px; background: #f8fafc; border-bottom: 1px solid #e2e8f0; font-family: sans-serif; align-items: center;">
      <span style="font-weight: bold; font-size: 1.1rem; color: #0f172a;">SkinLab</span>
      <NuxtLink to="/" style="text-decoration: none; color: #0284c7; font-weight: 500;">Home</NuxtLink>
      <NuxtLink to="/about" style="text-decoration: none; color: #0284c7; font-weight: 500;">About</NuxtLink>
      <NuxtLink to="/contact" style="text-decoration: none; color: #0284c7; font-weight: 500;">Contact</NuxtLink>
    </nav>
    <NuxtPage />
  </div>
</template>
