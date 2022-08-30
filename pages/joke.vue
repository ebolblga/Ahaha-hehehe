<script setup lang="ts">
useHead({ title: "Генератор анекдотов" });
let chain;
let notificationHidden = ref(true);

onMounted(async () => {
  chain = await $fetch("/jokeChain.json");
  genJoke();
});
const iRandom = (max) => ~~(Math.random() * max);
function generate() {
  const words = [];
  const start = [
    ...(chain["."] ? Object.keys(chain["."]) : []),
    ...(chain["?"] ? Object.keys(chain["?"]) : []),
    ...(chain["!"] ? Object.keys(chain["!"]) : []),
  ];
  let word = "";
  const endMark = { ".": 1, "?": 1, "!": 1, "!!!": 1 };
  while (1) {
    if (word == "") {
      word = start[iRandom(start.length)];
      words.push(word);
      continue;
    }
    if (endMark[word]) {
      break;
    }
    const Words = chain[word];
    const values: number[] = Object.values(Words);
    const sum = values.reduce((acc, v) => acc + v, 0);
    let num = iRandom(sum);
    const i = values.reduce((acc, v) => {
      num -= v;
      if (num < 0) return acc;
      return acc + 1;
    }, 0);
    word = Object.keys(Words)[i];
    words.push(word);
  }
  return words.join(" ").replace(/ [?.!:,]{1,3}/g, (value) => value.slice(1));
}

let joke = ref("");
function genJoke() {
  joke.value = generate();
}

async function copyJoke() {
  try {
    await navigator.clipboard.writeText(joke.value.charAt(0).toUpperCase() + joke.value.slice(1));
    //alert('Copied');
  } catch ($e) {
    alert("Cannot copy");
  }
}
</script>

<template>
  <div class="flex justify-center content-center text-center pt-[5vh] mx-10">
  <div>
    <my-button @click="genJoke">Сгенерировать</my-button>
    <p class="text-xl mt-10 drop-shadow-xl">
      {{ joke.charAt(0).toUpperCase() + joke.slice(1) }}
    </p>
    <my-button-sm
        @click="copyJoke(), (notificationHidden = false)"
        class="mt-14"
      >
        Копировать анекдот
        <span class="material-symbols-outlined material-icons md-18">
          link
        </span>
      </my-button-sm>
  </div>
  <alert
      :class="{
        'ok bottom-10 fixed mx-auto animation': true,
        hidden: notificationHidden,
      }"
      @click="notificationHidden = true"
      >Анекдот скопирован!</alert
    >
  </div>
</template>
