<script setup lang="ts">
const {public:{base}} = useRuntimeConfig()
useHead({
  link:[{
    rel:"icon",
    href:`${base}favicon.ico`,
    type:"image/x-icon"
  }]
})
</script>

<template>
  <div class="h-screen">
    <Navbar />
    <slot />
  </div>
</template>

<style>
body {
  background: linear-gradient(0deg, #FFE66B, #FFC15E);
  color: #373F41;
}
</style>