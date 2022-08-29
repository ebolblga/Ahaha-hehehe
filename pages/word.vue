<script setup lang="ts">
useHead({ title: "Генератор слов" });

// function getWord() {
//   const fs = require("fs/promises");
//   const s1 = ["Д", "Б", "Х", "П"];
//   const s2 = ["аб", "об", "уб", "ыб", "еб", "иб"];
//   A = ["Пип", "Зелеб", "Еб", "Ебол", "Хеб", "Поп", "А", "Е"];
//   B = ["у", "ы", "е", "о", "боб"];
//   C = ["лда", "га", "ба", "нга", "ун", "ан", "ук", "он"];
//   const words = [];
//   A.forEach(a => B.forEach(b=>C.forEach(c => words.push(a + b + c))));
//   s1.forEach(a=>s2.forEach(a1=>B.forEach(b=>C.forEach(c => words.push(a + a1 + b + c)))));
//   console.log(words);
//   fs.writeFile("./Library/ebeba.txt", words.join("\n"));
// }
</script>

<template>
  <div class="content-center text-center pt-[5vh]">
    <my-button @click="">Сгенерировать</my-button>
  </div>
</template>
