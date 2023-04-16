<template>
  <header :class="['w-full', 'text-lg', 'font-bold']">
    <div class="fixed bottom-0 left-0 h-16 w-full bg-black/75 text-white">
      <div class="h-full w-full border-t border-solid border-brand-gray-1">
        <ul class="flex h-full list-none items-center justify-center">
          <li class="ml-9 h-full first:ml-0">
            <h3 class="flex h-full items-center py-2.5 hover:text-brand-pink-1">
              Hello
            </h3>
          </li>
        </ul>
      </div>
    </div>
  </header>
</template>

<script lang="ts" setup></script>
