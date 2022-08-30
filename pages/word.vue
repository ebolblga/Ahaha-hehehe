<script setup lang="ts">
useHead({ title: "Генератор слов" });

onMounted(async () => {
  getWord();
});

function genWord() {
  if (randomIntFromInterval(0, 399) == 0) {
    const bonus = ["Похороны", "Абоба"];
    return bonus[randomIntFromInterval(0, 1)];
  }

  const altStart1 = ["Д", "Б", "Х", "П"];
  let altStart = altStart1[randomIntFromInterval(0, altStart1.length - 1)];

  const altStart2 = ["аб", "об", "уб", "ыб", "еб", "иб"];
  altStart += altStart2[randomIntFromInterval(0, altStart2.length - 1)];

  const A = [altStart, "Пип", "Зелеб", "Еб", "Ебол", "Поп"];
  let word = A[randomIntFromInterval(0, A.length - 1)];

  const B = ["у", "ы", "е", "о", "боб"];
  word += B[randomIntFromInterval(0, B.length - 1)];

  const C = ["лда", "га", "ба", "нга", "лдочка"];
  word += C[randomIntFromInterval(0, C.length - 1)];

  return word;
}

let word = ref("");
function getWord() {
  word.value = genWord();
}

function randomIntFromInterval(min, max) {
  return Math.floor(Math.random() * (max - min + 1) + min);
}
</script>

<template>
  <div class="content-center text-center pt-[5vh] mx-10">
    <my-button @click="getWord()">Сгенерировать</my-button>
    <p class="text-3xl mt-10 drop-shadow-xl">
      {{ word }}
    </p>
  </div>
</template>
