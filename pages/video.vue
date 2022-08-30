<script setup lang="ts">
import axios from "axios";

useHead({ title: "Генератор видео" });
const videoIds = ref<string[]>([]);
function genId(length) {
  let result = "";
  const characters =
    "0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz-_";
  for (let i = 0; i < length; i++) {
    result += characters.charAt(Math.floor(Math.random() * characters.length));
  }
  return result;
}

async function findVid(length = 3) {
  const query = genId(length);
  const html: string = (
    await axios.get(
      `https://api.allorigins.win/get?url=${encodeURIComponent(
        "https://www.youtube.com/results?search_query=" + query
      )}`
    )
  ).data.contents;

  videoIds.value = [
    ...new Set([...html.matchAll(/\"videoId\":\"(.+?)\"/g)].map(([, a]) => a)),
  ];
}

onMounted(async () => {
  findVid(5);
});
</script>

<template>
  <div class="flex justify-center content-center text-center pt-[5vh] mx-10">
    <div>
      <my-button @click="findVid(5)">Найти</my-button>
      <iframe
        :src="`https://www.youtube.com/embed/${
          videoIds[~~(Math.random() * videoIds.length)]
        }`"
        class="mt-7 shadow-xl bg-black lg:w-[854px] lg:h-[480px] md:w-[640px] md:h-[360px]"
        frameborder="0"
        allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
        allowfullscreen
      ></iframe>
      <my-button @click="findVid(5)" class="mt-7">
      Копировать ссылку
      <span class="material-symbols-outlined">
        link
      </span>
      </my-button>
    </div>
  </div>
</template>

<style>
  .material-symbols-outlined {
    font-variation-settings:
    'FILL' 1,
    'wght' 700,
    'GRAD' 200,
    'opsz' 48
  }
  </style>