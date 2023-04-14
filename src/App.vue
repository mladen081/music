<template>
  <main-nav />
  <router-view />
</template>

<script lang="ts" setup>
import MainNav from "@/components/Navigation/MainNav.vue";
</script>

<style>
body {
  font-size: 1.4em;
}
h1 {
  font-size: 2em;
  text-transform: uppercase;
  color: #fff;
  margin: 20px 0;
  text-align: center;
}

@media (max-width: 767px) {
  body {
    font-size: 1.2em;
  }
  h1 {
    font-size: 1.5em;
  }
}
</style>
