<template>
  <div class="text-white relative">
    <button class="flex justify-between p-4 rounded-lg bg-sky-500 items-center w-[100px]" id="button-menu" @click="toggleMenu">
      <span>Menu</span>
      <i class="fa-solid fa-chevron-down"></i>
    </button>

    <div v-if="isActive" :class="`w-[300px] shadow-lg py-2 rounded-md absolute top-full right-0 bg-[#272B34]`">
      <div class="w-full">
        <a href="#" class="flex items-center gap-4 w-full hover:bg-black hover:backdrop-opacity-15 py-2 px-5">
          <i class="fa-regular fa-file"></i>
          <span>Download XLS</span>
        </a>
        <a href="#" class="flex items-center gap-4 w-full hover:bg-black hover:backdrop-opacity-15 py-2 px-5">
          <i class="fa-solid fa-chart-column"></i>
          <span>Set Trend Sub Keg</span>
        </a>
        <a href="#" class="flex items-center gap-4 w-full hover:bg-black hover:backdrop-opacity-15 py-2 px-5">
          <i class="fa-solid fa-chart-column"></i>
          <span>Set Trend Daerah</span>
        </a>
        <a href="#" class="flex items-center gap-4 w-full hover:bg-black hover:backdrop-opacity-15 py-2 px-5">
          <i class="fa-regular fa-circle-play"></i>
          <span>Indikator Kinerja</span>
        </a>
      </div>
      <div class="w-full h-[2px] bg-black"></div>
      <div class="w-full">
        <a href="#" class="flex items-center gap-4 w-full hover:bg-black hover:backdrop-opacity-15 py-2 px-5">
          <i class="fa-regular fa-file"></i>
          <span>RKPD</span>
        </a>
        <a href="#" class="flex items-center gap-4 w-full hover:bg-black hover:backdrop-opacity-15 py-2 px-5">
          <i class="fa-solid fa-chart-column"></i>
          <span>RKPD - KUA/PPAS - APBD</span>
        </a>
      </div>
    </div>
  </div>
</template>

<script lang="ts" setup>
const isActive = ref(false);

const toggleMenu = () => {
  isActive.value = !isActive.value;
};

onMounted(() => {
  window.addEventListener("click", function (event: MouseEvent) {
    const targetElement = event.target as HTMLElement;

    if (!targetElement.closest("#button-menu")) {
      isActive.value = false;
    }
  });
});
</script>
