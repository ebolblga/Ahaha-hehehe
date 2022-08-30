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
  <head>
    <link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Material+Symbols+Outlined:opsz,wght,FILL,GRAD@20..48,100..700,0..1,-50..200" />
  </head>
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