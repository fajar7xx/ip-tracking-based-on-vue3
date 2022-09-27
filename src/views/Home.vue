<script setup></script>

<template>
  <div class="flex flex-col h-screen max-h-screen">
    <!-- searh result -->
    <div
      class="relative flex justify-center px-4 pt-8 pb-32 bg-cover bg-hero-pattern"
    >
      <!-- search input -->
      <div class="w-full max-w-screen-sm">
        <h1 class="pb-4 text-3xl text-center text-white">IP Address Tracker</h1>
        <div class="flex">
          <input
            type="text"
            name="ip"
            id="ip"
            class="flex-1 px-2 py-3 rounded-tl-md rounded-bl-md focus:outline-none"
            placeholder="Search for any ip address or leave empty to get your ip info"
          />
          <i class="flex items-center px-4 text-white bg-black cursor-pointer fa-solid fa-chevron-right rounded-tr-md rounded-br-md"></i>
        </div>
      </div>
    </div>
  </div>
</template>
