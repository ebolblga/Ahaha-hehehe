<script setup lang="ts">
import axios from "axios";
import parse from "node-html-parser";

useHead({ title: "Генератор видео" });
const videoIds = ref<string[]>([])
function genId(length) {
  let result = "";
  const characters =
    "0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz-_";
  for (let i = 0; i < length; i++) {
    result += characters.charAt(Math.floor(Math.random() * characters.length));
  }
  console.log(result);
  return result;
}
function txtDownload(text, name = "test.html") {
  const a = document.createElement("a")
  a.download = name
  a.href = URL.createObjectURL(new Blob([text], { type: "application/html" }))
  a.click()
}
async function findVid(length = 3) {
  const query = genId(length);
  const html: string = (
    await axios.get(`https://api.allorigins.win/get?url=${encodeURIComponent('https://www.youtube.com/results?search_query=' + query)}`)
    //await axios.get(`https://thingproxy.freeboard.io/fetch/https://www.youtube.com/results?search_query=${query}`)
  ).data.contents;

  videoIds.value = [...new Set([...html.matchAll(/\"videoId\":\"(.+?)\"/g)].map(([, a]) => a))]
}
</script>

<template>
  <div class="content-center text-center pt-[5vh]">
    <my-button @click="findVid(5)">Найти</my-button>
    <iframe width="1280" height="720" v-for="id in videoIds" :src="`https://www.youtube.com/embed/${id}`" frameborder="0"
      allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
      allowfullscreen></iframe>
  </div>
</template>