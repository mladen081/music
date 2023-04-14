<template>
  <header :class="['w-full', 'text-lg', 'font-bold']">
    <div class="fixed top-0 left-0 h-16 w-full bg-black/75 text-white">
      <div
        class="mx-auto flex h-full flex-nowrap border-b border-solid border-brand-gray-1 px-8"
      >
        <nav class="h-full w-full">
          <ul class="flex h-full list-none items-center justify-center">
            <li
              v-for="menuItem in menuItems"
              :key="menuItem.text"
              class="ml-9 h-full first:ml-0"
            >
              <router-link
                :to="menuItem.url"
                class="flex h-full items-center py-2.5 hover:text-brand-pink-1"
                >{{ menuItem.text }}</router-link
              >
            </li>
          </ul>
        </nav>
      </div>
    </div>
  </header>
</template>

<script lang="ts" setup>
import { ref } from "vue";

const menuItems = ref([
  { text: "HOME", url: "/" },
  { text: "CONTACT", url: "/contact" },
]);
</script>
