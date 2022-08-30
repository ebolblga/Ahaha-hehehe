<script setup lang="ts">
useHead({ title: "Генератор анекдотов" });
let chain;

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
</script>

<template>
  <div class="content-center text-center pt-[5vh] mx-10">
    <my-button @click="genJoke">Сгенерировать</my-button>
    <p class="text-xl mt-10 drop-shadow-xl">
      {{ joke.charAt(0).toUpperCase() + joke.slice(1) }}
    </p>
  </div>
</template>
