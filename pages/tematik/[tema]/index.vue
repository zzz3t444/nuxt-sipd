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
    selectAll: false,
  },
  {
    id: 2,
    name: "AUDITOR",
    slug: "AUDITOR",
    anggaranP: "Rp 1.500.000.000",
    anggaranK: "Rp 2.500.000.000",
    showDropdown: false,
    selectedProvinces: [],
    selectAll: false,
  },
  {
    id: 3,
    name: "BENCANA",
    slug: "BENCANA",
    anggaranP: "Rp 4.500.000.000",
    anggaranK: "Rp 2.500.000.000",
    showDropdown: false,
    selectedProvinces: [],
    selectAll: false,
  },
  {
    id: 4,
    name: "	SIGA",
    slug: "	SIGA",
    anggaranP: "Rp 4.500.000.000",
    anggaranK: "Rp 2.400.000.000",
    showDropdown: false,
    selectedProvinces: [],
    selectAll: false,
  },
]);

const provinces = ref([
  { id: 1, name: "Aceh", checked: false },
  { id: 2, name: "Sumatera Utara", checked: false },
  { id: 3, name: "Sumatera Barat", checked: false },
  { id: 4, name: "Riau", checked: false },
  { id: 5, name: "Jambi", checked: false },
  { id: 6, name: "Sumatera Selatan", checked: false },
  { id: 7, name: "Bengkulu", checked: false },
  { id: 8, name: "Lampung", checked: false },
  { id: 9, name: "Kepulauan Bangka Belitung", checked: false },
  { id: 10, name: "Kepulauan Riau", checked: false },
  { id: 11, name: "DKI Jakarta", checked: false },
  { id: 12, name: "Jawa Barat", checked: false },
  { id: 13, name: "Jawa Tengah", checked: false },
  { id: 14, name: "DI Yogyakarta", checked: false },
  { id: 15, name: "Jawa Timur", checked: false },
  { id: 16, name: "Banten", checked: false },
  { id: 17, name: "Bali", checked: false },
  { id: 18, name: "Nusa Tenggara Barat", checked: false },
  { id: 19, name: "Nusa Tenggara Timur", checked: false },
  { id: 20, name: "Kalimantan Barat", checked: false },
  { id: 21, name: "Kalimantan Tengah", checked: false },
  { id: 22, name: "Kalimantan Selatan", checked: false },
  { id: 23, name: "Kalimantan Timur", checked: false },
  { id: 24, name: "Kalimantan Utara", checked: false },
  { id: 25, name: "Sulawesi Utara", checked: false },
  { id: 26, name: "Sulawesi Tengah", checked: false },
  { id: 27, name: "Sulawesi Selatan", checked: false },
  { id: 28, name: "Sulawesi Tenggara", checked: false },
  { id: 29, name: "Gorontalo", checked: false },
  { id: 30, name: "Sulawesi Barat", checked: false },
  { id: 31, name: "Maluku", checked: false },
  { id: 32, name: "Maluku Utara", checked: false },
  { id: 33, name: "Papua Barat", checked: false },
  { id: 34, name: "Papua", checked: false },
  { id: 35, name: "Papua Tengah", checked: false },
  { id: 36, name: "Papua Pegunungan", checked: false },
  { id: 37, name: "Papua Selatan", checked: false },
  { id: 38, name: "Papua Barat Daya", checked: false },
]);

const toggleDropdown = (prov) => {
  prov.showDropdown = !prov.showDropdown;
};

const toggleCheckbox = (province, prov) => {
  province.checked = !province.checked;

  if (province.checked) {
    if (!prov.selectedProvinces.includes(province.name)) {
      prov.selectedProvinces.push(province.name);
    }
  } else {
    prov.selectedProvinces = prov.selectedProvinces.filter((name) => name !== province.name);
  }

  prov.selectAll = provinces.value.every((p) => p.checked);
};

const toggleSelectAll = (prov) => {
  prov.selectAll = !prov.selectAll;
  provinces.value.forEach((province) => {
    province.checked = prov.selectAll;
    if (prov.selectAll) {
      if (!prov.selectedProvinces.includes(province.name)) {
        prov.selectedProvinces.push(province.name);
      }
    } else {
      prov.selectedProvinces = [];
    }
  });
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
                <td class="py-3 px-5">{{ prov.name }}</td>
                <td class="py-3 px-5 text-center">
                  <button @click="toggleDropdown(prov)" class="text-blue-500">
                    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="2" stroke="currentColor" class="w-4 h-4 inline">
                      <path stroke-linecap="round" stroke-linejoin="round" d="M19 9l-7 7-7-7" />
                    </svg>
                  </button>
                  {{ prov.anggaranP }}

                  <!-- Dropdown provinsi dengan checkbox -->
                  <div v-if="prov.showDropdown" class="absolute bg-white border border-gray-300 shadow-lg mt-2 w-60 max-h-60 overflow-y-auto">
                    <ul>
                      <li class="flex items-center p-2 hover:bg-gray-100">
                        <input type="checkbox" :checked="prov.selectAll" @change="toggleSelectAll(prov)" />
                        <span class="ml-2">Select All</span>
                      </li>
                      <li v-for="province in provinces" :key="province.id" class="flex items-center p-2 hover:bg-gray-100">
                        <input type="checkbox" v-model="province.checked" @change="toggleCheckbox(province, prov)" />
                        <span class="ml-2">{{ province.name }}</span>
                      </li>
                    </ul>
                  </div>

                  <!-- Menampilkan provinsi yang dipilih -->
                  <div v-if="prov.selectedProvinces.length" class="mt-1 text-sm text-gray-600">{{ prov.selectedProvinces.length }} terpilih</div>
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
          <h1 class="text-md mt-10 font-medium">Data Update : 20 Juli 2024</h1>
        </div>
      </div>
    </div>
    <TabsSystem />
  </div>
  <NuxtPage v-else />
</template>

<style scoped>
.absolute {
  position: absolute;
}
</style>
