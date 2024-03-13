<script setup>
import IPInfo from '@/components/IPInfo.vue'
</script>

<template>
  <main>
    <div class="flex flex-col h-screen max-h-screen">
      <!-- Search / Results -->
      <div class="flex justify-center bg-hero-pattern bg-cover relative px-4 pt-8 pb-32">
        <!-- Search Input -->
        <div class="w-full max-w-screen-sm">
          <h1 class="text-white text-center text-3xl pb-4">IP Address Tracker</h1>
          <div class="flex">
            <input 
              type="text"
              class="flex-1 py-3 px-2 rounded-tl-md rounded-bl-md focus:outline-none"
              placeholder="Search for any IP address or leave empty to get your IP information"
            >
            <i class="fa-solid fa-arrow-right 
            cursor-pointer bg-black text-white rounded-tr-md rounded-br-md flex items-center px-4"></i>
          </div>
        </div>
        <!-- IP Info -->
        <IPInfo />
      </div>
    </div>
  </main>
</template>
