<template>
  <div id="app">
    <!-- <NuxtLoadingIndicator /> -->
    <NuxtRouteAnnouncer />
    <Header />
    <NuxtPage class="main" />
  </div>
</template>

<script setup>
import Header from './components/common/Header.vue';
const config = useAppConfig()
useSeoMeta({
  title: config.title
})
</script>

<style>
.page-enter-active,
.page-leave-active {
  transition: all 0.4s;
}
.page-enter-from,
.page-leave-to {
  opacity: 0;
  filter: blur(1rem);
}
</style>
