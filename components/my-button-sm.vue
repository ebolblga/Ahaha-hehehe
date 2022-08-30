<template>
  <button
    type="button"
    class="px-3 py-1 focus:outline-none rounded-full focus:z-10 bg-white text-[#373F41] hover:text-black hover:bg-yellow-200 select-none shadow-md active:scale-95"
  >
    <slot />
  </button>
</template>

<style>
.shake {
  animation: shake-animation 3s ease-in-out;
  transform-origin: 50% 50%;
}

@keyframes shake-animation {
  0% {
    transform: translate(0, 0);
  }
  1.78571% {
    transform: translate(4px, 1px);
  }
  3.57143% {
    transform: translate(0, -1px);
  }
  5.35714% {
    transform: translate(5px, 1px);
  }
  7.14286% {
    transform: translate(0, 0);
  }
  8.92857% {
    transform: translate(3px, -1px);
  }
  10.71429% {
    transform: translate(0, 0);
  }
  100% {
    transform: translate(0, 0);
  }
}
</style>
