<script setup>
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <main class="relative max-w-[540px] mx-auto border h-[100vh] p-3 bg-zinc-900 text-white">
    <div class="flex items-center justify-between py-3 border-b">
      <button>
        burger
      </button>
      <RouterLink to="/" class="font-bold text-xl">Noted</RouterLink>
      <div>search</div>
    </div>
    <RouterView />

   <router-link to="/create" 
   class="border px-3 py-1 text-center rounded-full absolute bottom-3
    right-3 bg-red-600 text-white text-2xl">+</router-link>
  </main>
  
</template>

