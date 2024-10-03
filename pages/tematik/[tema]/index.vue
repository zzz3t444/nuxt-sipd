<script setup>
import { ref } from "vue";
import { useRoute } from "vue-router";

const route = useRoute();

const provinsiList = ref([
  {
    id: 1,
    name: "ANGKUTAN ORANG",
    slug: "ANGKUTAN ORANG",
    anggaranP: "Rp 1.000.000.000",
    anggaranK: "Rp 2.000.000.000",
    showDropdown: false, 
    selectedProvinces: [], 
  },
  {
    id: 2,
    name: "AUDITOR",
    slug: "AUDITOR",
    anggaranP: "Rp 1.500.000.000",
    anggaranK: "Rp 2.500.000.000",
    showDropdown: false,
    selectedProvinces: [], 
  },
  {
    id: 3,
    name: "BENCANA",
    slug: "BENCANA",
    anggaranP: "Rp 4.500.000.000",
    anggaranK: "Rp 2.500.000.000",
    showDropdown: false,
    selectedProvinces: [], 
  },
]);

const provinces = ref([
  { id: 1, name: "Province A", checked: false },
  { id: 2, name: "Province B", checked: false },
  { id: 3, name: "Province C", checked: false },
  { id: 4, name: "Province D", checked: false },
  { id: 5, name: "Province E", checked: false },
  { id: 6, name: "Province F", checked: false },
  { id: 7, name: "Province G", checked: false },
  { id: 8, name: "Province H", checked: false },
  { id: 9, name: "Province I", checked: false },
  { id: 10, name: "Province J", checked: false },
  { id: 11, name: "Province K", checked: false },
  { id: 12, name: "Province L", checked: false },
  { id: 13, name: "Province M", checked: false },
  { id: 14, name: "Province N", checked: false },
  { id: 15, name: "Province O", checked: false },
  { id: 16, name: "Province P", checked: false },
  { id: 17, name: "Province Q", checked: false },
  { id: 18, name: "Province R", checked: false },
  { id: 19, name: "Province S", checked: false },
  { id: 20, name: "Province T", checked: false },
  { id: 21, name: "Province U", checked: false },
  { id: 22, name: "Province V", checked: false },
  { id: 23, name: "Province W", checked: false },
  { id: 24, name: "Province X", checked: false },
  { id: 25, name: "Province Y", checked: false },
  { id: 26, name: "Province Z", checked: false },
  { id: 27, name: "Province AA", checked: false },
  { id: 28, name: "Province AB", checked: false },
  { id: 29, name: "Province AC", checked: false },
  { id: 30, name: "Province AD", checked: false },
  { id: 31, name: "Province AE", checked: false },
  { id: 32, name: "Province AF", checked: false },
  { id: 33, name: "Province AG", checked: false },
  { id: 34, name: "Province AH", checked: false },
  { id: 35, name: "Province AI", checked: false },
  { id: 36, name: "Province AJ", checked: false },
  { id: 37, name: "Province AK", checked: false },
  { id: 38, name: "Province AL", checked: false },
]);

const toggleDropdown = (prov) => {
  prov.showDropdown = !prov.showDropdown;
};

const toggleCheckbox = (province, prov) => {
  province.checked = !province.checked;
  if (province.checked) {
    // Add province to selected list
    prov.selectedProvinces.push(province.name);
  } else {
    // Remove province from selected list
    prov.selectedProvinces = prov.selectedProvinces.filter((name) => name !== province.name);
  }
};
</script>

<template>
  <div v-if="!route.params.provinsi">
    <div class="flex justify-between items-center">
      <div>
        <h1 class="text-2xl text-black">Tematik</h1>
        <h1 class="text-sm text-neutral-500">
          <NuxtLink to="/" class="text-[#009efb] hover:text-[#7460e]">Dashboard</NuxtLink>
          /
          <NuxtLink to="/" class="text-[#009efb] hover:text-[#7460e]">Informasi Pembangunan Daerah</NuxtLink>
          /
          <NuxtLink to="/tematik" class="text-[#009efb] hover:text-[#7460e]">Tematik</NuxtLink>
          / {{ route.params.tema }}
        </h1>
      </div>
      <div>
        <SelectYear />
      </div>
    </div>
    <div class="bg-white w-full sm:px-5 py-4 rounded-2xl my-8">
      <div class="w-full bg-white px-7 rounded-lg text-black py-8">
        <EntriesValue />
        <div class="w-full mt-10 overflow-x-auto">
          <table class="w-full">
            <thead>
              <tr>
                <th class="px-4">No</th>
                <th class="px-4">Tema</th>
                <th class="px-4">Anggaran / Provinsi</th>
                <th class="px-4">%{?}</th>
                <th class="px-4">Anggaran / Kabupaten</th>
              </tr>
            </thead>
            <tbody>
              <tr class="border-t-[1px]" v-for="(prov, index) in provinsiList" :key="prov.id">
                <td class="py-3 px-5 text-center">{{ index + 1 }}</td>
                <td class="py-3 px-5">
                  <NuxtLink :to="`/tematik/${route.params.tema}/${prov.slug}`">
                    {{ prov.name }}
                  </NuxtLink>
                </td>
                <td class="py-3 px-5 text-center">
                  <button @click="toggleDropdown(prov)" class="text-blue-500">
                    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="2" stroke="currentColor" class="w-4 h-4 inline">
                      <path stroke-linecap="round" stroke-linejoin="round" d="M19 9l-7 7-7-7" />
                    </svg>
                  </button>
                  {{ prov.anggaranP }}
                  <div v-if="prov.showDropdown" class="absolute bg-white border border-gray-300 shadow-lg mt-2 w-48 max-h-60 overflow-y-auto">
                    <ul>
                      <li v-for="province in provinces" :key="province.id" class="flex items-center p-2 hover:bg-gray-100">
                        <input type="checkbox" v-model="province.checked" @change="toggleCheckbox(province, prov)" />
                        <span class="ml-2">{{ province.name }}</span>
                      </li>
                    </ul>
                  </div>
                  <div v-if="prov.selectedProvinces.length" class="mt-1 text-sm text-gray-600">Selected: {{ prov.selectedProvinces.join(", ") }}</div>
                </td>
                <td class="py-3 px-5 text-center">10%</td>
                <td class="py-3 px-5 text-center">{{ prov.anggaranK }}</td>
              </tr>
              <tr class="border-t-[2px] font-semibold">
                <td colspan="2" class="py-3 px-5 text-center">Total</td>
                <td class="py-3 px-5 text-center">230.000.000,00</td>
                <td class="py-3 px-5 text-center">10%</td>
                <td class="py-3 px-5 text-center">120.000.000,00</td>
              </tr>
            </tbody>
          </table>
          <h1 class="text-md mt-10 font-medium">Data Update : 20 juli 2024</h1>
        </div>
      </div>
    </div>

    <div class="mt-5 w-full bg-white py-12 px-7 rounded-2xl text-white">
      <h1 class="text-start font-bold text-black text-2xl">Per Tingkatan Pemerintah Daerah</h1>
      <div class="grid justify-center items-center gap-3 py-12">
        <div class="flex items-center text-black gap-3 text-xl">
          <ul class="p-3 w-5 bg-[#ff9000]"></ul>
          <p>provinsi</p>
        </div>
        <div class="flex items-center text-black gap-3 text-xl">
          <ul class="p-3 w-5 bg-[#009efb]"></ul>
          <p>Kab/Kota</p>
        </div>
      </div>
      <div class="flex flex-col gap-8 w-full px-4">
        <ChartCollapse bgcolor="bg-[#ff9000]" title="Provinsi" ckey="1" />
        <ChartCollapse bgcolor="bg-[#009efb]" title="Kab / Kota" ckey="2" />
      </div>
    </div>
  </div>
  <NuxtPage v-else />
</template>

<style scoped>
.absolute {
  position: absolute;
}
</style>
