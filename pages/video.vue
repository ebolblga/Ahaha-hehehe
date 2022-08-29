<script setup lang="ts">
import axios from "axios";
import parse from "node-html-parser";

useHead({ title: "Генератор видео" });

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

async function findVid(length = 3) {
  const query = genId(length);
  const html = (
    await axios.get(`https://api.allorigins.win/get?url=${encodeURIComponent('https://www.youtube.com/results?search_query=' + query)}`)  
  //await axios.get(`https://thingproxy.freeboard.io/fetch/https://www.youtube.com/results?search_query=${query}`)
  ).data;
  //const document = parse(html);
  const a = document.createElement("div");
  a.innerHTML=html;
  const words = Array.from(a.querySelectorAll("#video-title"));
  console.log(words);
  
}
</script>

<template>
  <div class="content-center text-center pt-[5vh]">
    <my-button @click="findVid(5)">Найти</my-button>
  </div>
</template>