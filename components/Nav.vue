
<script setup>
import { onMounted, ref } from "vue";
import '../assets/css/font.css'

const bars = ref(null);
const smollBar = ref(null);
const hiddenList = ref([]);
const isPembangunanSubmenuOpen = ref(false);
const isProvinceSubmenuOpen = ref(false);
const isKabKotaSubmenuOpen = ref(false);

const toggleKabKotaSubmenu = () => {
  isKabKotaSubmenuOpen.value = !isKabKotaSubmenuOpen.value;
};

const toggleProvinceSubmenu = () => {
  isProvinceSubmenuOpen.value = !isProvinceSubmenuOpen.value;
};

const togglePembangunanSubmenu = () => {
  isPembangunanSubmenuOpen.value = !isPembangunanSubmenuOpen.value;
};

onMounted(() => {
  bars.value = document.getElementById("bars");
  smollBar.value = document.getElementById("small-bar");
  hiddenList.value = document.querySelectorAll(".hidden-list");

  if (bars.value) {
    bars.value.onclick = () => {
      document.body.classList.toggle("active-navbar");
    };
  }

  if (smollBar.value) {
    smollBar.value.onclick = () => {
      document.body.classList.toggle("active-small-device-sidebar");
    };
  }

  hiddenList.value.forEach((item) => {
    item.onclick = () => {
      if (!item.classList.contains("province-submenu") && !item.classList.contains("kabkota-submenu")) {
        item.classList.toggle("active-list");
      }
    };
  });
});
</script>

<template>
  <div class="inter">
    <div class="group z-[1000]">
      <div
        class="sidebar md:group-hover:w-[225px] transition-all w-full md:w-[70px] h-[70px] fixed top-0 left-0 z-50 bg-white p-2 px-5 md:py-5 md:px-0 flex justify-between md:justify-center items-center gap-5 shadow-sm">
        <a href="#" class="text-neutral-700 block md:hidden" id="small-bar">
          <i class="fa-solid fa-bars"></i>
        </a>
        <div class="flex justify-center items-center w-full">
          <img class="w-10" src="../assets/images/logo.png" alt="logo" />
          <h1 class="text block md:hidden text-black font-bold text-2xl md:group-hover:block ml-2">SIPD</h1>
        </div>
        <div class="md:hidden"></div>
      </div>
      <div class="sidebar smoll fixed transition-all -left-[225px] md:left-0 top-[70px] h-screen max-h-screen w-[225px] md:w-[70px] bg-white z-40 flex flex-col md:group-hover:w-[225px] shadow-xl">
        <ul class="flex flex-col gap-7 py-5 overflow-y-auto no-scrollbar">
          <li class="px-5">
            <div class="text-neutral-700 block md:hidden text-nowrap font-medium uppercase md:group-hover:block">Menu Utama</div>
            <div class="text-neutral-700 hidden md:block text-center small-cap md:group-hover:hidden">...</div>
          </li>
          <li class="px-5">
            <div>
              <div class="text-neutral-700 font-bold text-center icon float-left md:float-none md:group-hover:float-left">
                <i class="fas fa-th-large"></i>
              </div>
              <NuxtLink class="text-neutral-700 pl-3 block md:hidden text-nowrap cap text-ellipsis overflow-hidden md:group-hover:block" to="/"> Dashboard </NuxtLink>
            </div>
          </li>
          <li class="px-5">
            <div>
              <div class="text-neutral-700 font-bold text-center icon md:float-none float-left md:group-hover:float-left">
                <i class="fa-solid fa-folder"></i>
              </div>
              <NuxtLink class="text-neutral-700 pl-3 block md:hidden text-nowrap cap text-ellipsis overflow-hidden md:group-hover:block" to="/rekap"> Rekap </NuxtLink>
            </div>
          </li>
          <li class="px-5 hidden-list" id="hidden-list">
            <a href="#" class="collappse flex items-center md:block md:group-hover:flex md:group-hover:items-center" @click.prevent="togglePembangunanSubmenu">
              <div class="text-neutral-700 text-center icon float-left md:float-none md:group-hover:float-left">
                <i class="fa-solid fa-circle-info"></i>
              </div>
              <div class="text-neutral-700 pl-3 block md:hidden text-nowrap cap text-ellipsis overflow-hidden md:group-hover:block">Informasi Pembangunan</div>
              <i class="fa-solid fa-chevron-left block md:hidden cap text-neutral-700 ml-2 arrow transition-all md:group-hover:block" :class="{ '-rotate-90': isPembangunanSubmenuOpen }"> </i>
            </a>
            <ul v-show="isPembangunanSubmenuOpen" class="flex flex-col gap-7 py-7">
              <li class="">
                <NuxtLink to="/tematik">
                  <div class="text-neutral-700 block md:hidden text-nowrap cap px-7 md:group-hover:block">Tematik</div>
                  <div class="text-neutral-700 text-center hidden md:block small-cap md:group-hover:hidden">
                    <i class="fa-solid fa-tag"></i>
                  </div>
                </NuxtLink>
              </li>
              <li class="">
                <NuxtLink to="/bidang_urusan">
                  <div class="text-neutral-700 block md:hidden text-nowrap cap px-7 md:group-hover:block">Bidang Urusan</div>
                  <div class="text-neutral-700 text-center hidden md:block small-cap md:group-hover:hidden">
                    <i class="fa-solid fa-tag"></i>
                  </div>
                </NuxtLink>
              </li>
              <li class="">
                <NuxtLink to="/sumber_pendanaan">
                  <div class="text-neutral-700 block md:hidden text-nowrap cap px-7 md:group-hover:block">Sumber Pendanaan</div>
                  <div class="text-neutral-700 text-center hidden md:block small-cap md:group-hover:hidden">
                    <i class="fa-solid fa-circle-dollar-to-slot"></i>
                  </div>
                </NuxtLink>
              </li>
            </ul>
          </li>
          <li class="border-t-2 border-slate-400"></li>
          <li class="px-5">
            <div class="text-neutral-700 block md:hidden text-nowrap font-medium uppercase md:group-hover:block">Provinsi</div>
            <div class="text-neutral-700 hidden md:block text-center small-cap md:group-hover:hidden">...</div>
          </li>
          <li class="px-5 hidden-list">
            <a
              href="#"
              class="collappse flex md:block items-center justify-between md:group-hover:flex md:group-hover:items-center md:group-hover:justify-between"
              @click.prevent="toggleProvinceSubmenu">
              <div class="text-neutral-700 text-center icon float-left md:float-none md:group-hover:float-left flex items-center md:block md:group-hover:flex md:group-hover:items-center collapse-title">
                <i class="fa-solid fa-location-pin"></i>
                <div class="text-neutral-700 pl-3 block md:hidden text-nowrap cap text-ellipsis overflow-hidden md:group-hover:block">ACEH</div>
              </div>
              <i class="fa-solid fa-chevron-left block md:hidden cap text-neutral-700 ml-2 arrow transition-all md:group-hover:block" :class="{ '-rotate-90': isProvinceSubmenuOpen }"></i>
            </a>
            <ul v-show="isProvinceSubmenuOpen" class="flex flex-col gap-7 py-7">
              <li class="">
                <NuxtLink to="/dashboard/aceh">
                  <div class="text-neutral-700 block md:hidden text-nowrap cap px-7 md:group-hover:block">Data Provinsi</div>
                  <div class="text-neutral-700 hidden md:block text-center small-cap md:group-hover:hidden">
                    <i class="fa-solid fa-tag"></i>
                  </div>
                </NuxtLink>
              </li>
              <li class="hidden-list" id="hidden-list">
                <a
                  href="#"
                  class="px-5 collappse flex md:block items-center justify-between md:group-hover:flex md:group-hover:items-center md:group-hover:justify-between"
                  @click.prevent="toggleKabKotaSubmenu">
                  <div class="text-neutral-700 text-center icon float-left md:float-none md:group-hover:float-left flex items-center md:block md:group-hover:flex md:group-hover:items-center collapse-title">
                    <div class="text-neutral-700 px-2 block md:hidden text-nowrap cap text-ellipsis overflow-hidden md:group-hover:block">Data Per Kab/Kota</div>
                  </div>

                  <i class="fa-solid fa-chevron-left block md:hidden cap text-neutral-700 ml-2 arrow transition-all md:group-hover:block" :class="{ '-rotate-90': isKabKotaSubmenuOpen }"></i>
                </a>
                <div class="text-neutral-700 hidden md:block text-center small-cap md:group-hover:hidden">
                  <i class="fa-solid fa-tag"></i>
                </div>
                <ul v-show="isKabKotaSubmenuOpen" class="flex flex-col gap-7 py-7 px-5">
                  <li class="">
                    <NuxtLink to="/dashboard/aceh/rekap">
                      <div class="text-neutral-700 block md:hidden text-nowrap cap px-7 md:group-hover:block">Rekap Aceh</div>
                      <div class="text-neutral-700 hidden md:block text-center small-cap md:group-hover:hidden"></div>
                    </NuxtLink>
                  </li>
                  <li class="">
                    <NuxtLink to="/dashboard/aceh/aceh selatan">
                      <div class="text-neutral-700 block md:hidden text-nowrap cap px-7 md:group-hover:block">aceh selatan</div>
                      <div class="text-neutral-700 hidden md:block text-center small-cap md:group-hover:hidden"></div>
                    </NuxtLink>
                  </li>
                </ul>
              </li>
            </ul>
          </li>
        </ul>
      </div>
    </div>

    <div
      class="z-10 fixed top-0 left-0 w-screen h-[70px] flex bg-gradient-to-r from-[#0178bc] to-[#00bdda] topbar after:absolute after:w-full after:top-0 after:left-0 after:bg-[url('/assets/images/pattern.png')] after:bg-contain after:h-full after:opacity-60">
      <div class="w-[70px] space"></div>
      <div class="flex justify-between items-center px-5">
        <a href="#" class="text-neutral-700 absolute z-50" id="bars">
          <i class="fa-solid fa-bars"></i>
        </a>
      </div>
    </div>
  </div>
</template>

