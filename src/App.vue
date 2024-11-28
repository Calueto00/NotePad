<script setup>
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <main class="relative max-w-[540px] mx-auto border h-[100vh] p-3">
    <div class="flex items-center justify-between py-3 border-b mb-2">
      <button>
        burger
      </button>
      <RouterLink to="/" class="font-bold text-xl">Noted</RouterLink>
      <div>search</div>
    </div>
    <RouterView />

   <router-link to="/create" 
   class="border px-3 py-1 text-center rounded-full fixed bottom-[10%]
    left bg-red-600 text-white text-2xl">+</router-link>
  </main>
  
</template>

