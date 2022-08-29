<script setup>
let isPressed = ref(true);
let isActive = ref(0);
</script>

<template>
  <div>
    <nav class="bg-white px-2 sm:px-4 py-2.5 rounded-lg w-[90vw] m-auto">
      <div
        class="container flex flex-wrap justify-between items-center mx-auto"
      >
        <NuxtLink to="/" @click="isActive = 0" class="flex items-center">
          <img src="/Logo.png" class="mr-3 h-6 sm:h-9" alt="Logo" />
        </NuxtLink>
        <div class="flex md:order-2">
          <button
            @click="isPressed = !isPressed"
            data-collapse-toggle="navbar-cta"
            type="button"
            class="inline-flex items-center p-2 text-sm rounded-lg md:hidden focus:outline-none focus:ring-2 text-gray-400 hover:bg-gray-700 focus:ring-gray-600"
            aria-controls="navbar-cta"
            aria-expanded="false"
          >
            <span class="sr-only">Открыть меню</span>
            <svg
              class="w-6 h-6"
              aria-hidden="true"
              fill="currentColor"
              viewbox="0 0 20 20"
              xmlns="http://www.w3.org/2000/svg"
            >
              <path
                fill-rule="evenodd"
                d="M3 5a1 1 0 011-1h12a1 1 0 110 2H4a1 1 0 01-1-1zM3 10a1 1 0 011-1h12a1 1 0 110 2H4a1 1 0 01-1-1zM3 15a1 1 0 011-1h12a1 1 0 110 2H4a1 1 0 01-1-1z"
                clip-rule="evenodd"
              ></path>
            </svg>
          </button>
        </div>
        <div
          class="justify-between items-center w-full md:flex md:w-auto md:order-1"
          :class="{ hidden: isPressed }"
          id="navbar-cta"
        >
          <ul
            class="flex flex-col p-4 mt-4 rounded-lg border md:flex-row md:space-x-8 md:mt-0 md:text-sm md:font-medium md:border-0 bg-white md:bg-white border-gray-700"
          >
            <li>
              <NuxtLink
                to="/meme"
                title="Генератор мемов"
                class="block py-2 pr-4 pl-3 md:p-0 text-gray-400 hover:bg-gray-700 hover:text-orange-500 md:hover:bg-transparent border-gray-700 hover:scale-105"
                :class="{ selected: ($route.name=='meme') }"
                aria-current="page"
                >Генератор мемов</NuxtLink
              >
            </li>
            <li>
              <NuxtLink
                to="/word"
                title="Субверсия языкового шаблона"
                class="block py-2 pr-4 pl-3 md:p-0 text-gray-400 hover:bg-gray-700 hover:text-orange-500 md:hover:bg-transparent border-gray-700 hover:scale-105"
                :class="{ selected: ($route.name=='word') }"
                >Генератор слов</NuxtLink
              >
            </li>
             <li>
              <NuxtLink
                to="/joke"
                title="Генерация анекдотов на основе цепи Маркова"
                class="block py-2 pr-4 pl-3 md:p-0 text-gray-400 hover:bg-gray-700 hover:text-orange-500 md:hover:bg-transparent border-gray-700 hover:scale-105"
                :class="{ selected: ($route.name=='joke') }"
                aria-current="page"
                >Генератор анекдотов</NuxtLink
              >
            </li>
            <li>
              <NuxtLink
                to="/video"
                title="Случайное видео из YouTube"
                class="block py-2 pr-4 pl-3 md:p-0 text-gray-400 hover:bg-gray-700 hover:text-orange-500 md:hover:bg-transparent border-gray-700 hover:scale-105"
                :class="{ selected: ($route.name=='video') }"
                >Генератор видео</NuxtLink
              >
            </li>
          </ul>
        </div>
      </div>
    </nav>
  </div>
</template>

<style>
.selected {
  color: rgb(255, 106, 68); 
}
.selected:hover {
  color: rgb(255, 90, 68); 
}
</style>