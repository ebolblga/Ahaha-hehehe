<script setup lang="ts">
import { isTSUndefinedKeyword } from "@babel/types";
import axios from "axios";

useHead({ title: "Генератор видео" });
const videoIds = ref<string[]>([]);
const id = ref<string>("");
const key = ref<string>("");
let notificationHidden = ref(true);

function genId(length) {
  let result = "";
  const characters =
    "0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz-_";
  for (let i = 0; i < length; i++) {
    result += characters.charAt(Math.floor(Math.random() * characters.length));
  }
  if (key.value.length > 0) {
    return key.value + " " + result;
  }

  return result;
}

async function findVid(length = 3) {
  const query = genId(length);
  console.log(query);
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
  id.value = videoIds.value[Math.floor(Math.random() * videoIds.value.length)];
}

onMounted(async () => {
  findVid(5);
});

async function copyURL() {
  try {
    await navigator.clipboard.writeText("https://youtu.be/" + id.value);
    //alert('Copied');
  } catch ($e) {
    alert("Cannot copy");
  }
}
</script>

<template>
  <div class="flex justify-center content-center text-center pt-[5vh] mx-10">
    <div>
      <my-button @click="findVid(5), notificationHidden = true">Найти</my-button>
      <input
        type="text"
        v-model="key"
        class="bg-gray-50 text-gray-900 text-sm rounded-lg block w-full p-2.5 border border-gray-300"
        placeholder="Ключевое слово"
        onkeydown="return /[a-zа-я]/i.test(event.key)"
      />
      <iframe
        :src="`https://www.youtube.com/embed/${id}`"
        class="mt-7 shadow-xl bg-black lg:w-[854px] lg:h-[480px] md:w-[640px] md:h-[360px]"
        frameborder="0"
        allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
        allowfullscreen
      ></iframe>
      <my-button-sm @click="copyURL(), notificationHidden = false" class="mt-14">
        Копировать ссылку
        <span class="material-symbols-outlined material-icons md-18">
          link
        </span>
      </my-button-sm>
    </div>
    <alert
      :class="{ 'ok bottom-10 fixed mx-auto animation': true, 'hidden': notificationHidden }"
      @click="notificationHidden = true"
      >Ссылка <u>https://youtu.be/{{ id }}</u> скопирована!</alert
    >
  </div>
</template>

<style>
.material-symbols-outlined {
  font-variation-settings: "FILL" 1, "wght" 700, "GRAD" 200, "opsz" 48;
}

.material-icons.md-18 {
  font-size: 18px;
  vertical-align: middle;
  padding-left: 7px;
}
</style>
