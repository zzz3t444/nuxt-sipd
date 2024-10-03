<script setup>
import { ref, computed } from "vue";

const temaList = ref([
  { id: 1, name: "ANGKUTAN ORANG", tema: "ANGKUTAN ORANG", national: "1.000.000.000,00", provincial: "1.200.000.000,00", district: "500.000.000,00" },
  { id: 2, name: "AUDITOR", tema: "AUDITOR", national: "800.000.000,00", provincial: "1.000.000.000,00", district: "400.000.000,00" },
  { id: 3, name: "BENCANA", tema: "BENCANA", national: "1.500.000.000,00", provincial: "1.800.000.000,00", district: "600.000.000,00" },
  { id: 4, name: "SIGA", tema: "SIGA", national: "900.000.000,00", provincial: "1.100.000.000,00", district: "450.000.000,00" },
  { id: 5, name: "SERTIFIKASI", tema: "SERTIFIKASI", national: "700.000.000,00", provincial: "900.000.000,00", district: "350.000.000,00" },
  { id: 6, name: "SISTEM MANAGEMENT", tema: "SISTEM MANAGEMENT", national: "1.200.000.000,00", provincial: "1.400.000.000,00", district: "550.000.000,00" },
]);

const selectedRows = ref([]);

const isAllSelected = computed(() => selectedRows.value.length === temaList.value.length && selectedRows.value.length > 0);

const toggleAll = () => {
  if (isAllSelected.value) {
    selectedRows.value = [];
  } else {
    selectedRows.value = temaList.value.map((item) => item.id);
  }
};
</script>

<template>
  <div class="flex justify-between items-center">
    <div class="">
      <h1 class="text-2xl text-black">Tematik</h1>
      <h1 class="text-sm text-neutral-500">
        <NuxtLink to="/" class="text-[#009efb] hover:text-[#7460e]">Dashboard</NuxtLink>
        /
        <NuxtLink to="/" class="text-[#009efb] hover:text-[#7460e]">Informasi Pembangunan Daerah</NuxtLink>
        / Tematik
      </h1>
    </div>
    <div class="">
      <SelectYear />
    </div>
  </div>

  <div class="bg-white w-full sm:px-5 py-4 rounded-2xl my-8 text-white">
    <div class="w-full bg-white px-7 rounded-lg text-black py-8">
      <EntriesValue />
      <div class="w-full mt-10 overflow-x-auto">
        <table class="w-full">
          <thead>
            <tr>
              <th class="px-4">
                <input type="checkbox" :checked="isAllSelected" @change="toggleAll" />
              </th>
              <th class="px-4">No</th>
              <th class="px-4">Tema</th>
              <th class="px-4">Nasional</th>
              <th class="px-4">%{?}</th>
              <th class="px-4">Provinsi</th>
              <th class="px-4">%{?}</th>
              <th class="px-4">Kab/Kota</th>
              <th class="px-4">%{?}</th>
            </tr>
          </thead>
          <tbody>
            <tr class="border-t-[1px]" v-for="(tema, index) in temaList" :key="tema.id">
              <td class="py-3 px-5 text-center">
                <input type="checkbox" :value="tema.id" v-model="selectedRows" />
              </td>
              <td class="py-3 px-5 text-center">{{ index + 1 }}</td>
              <td class="py-3 px-5">
                <NuxtLink :to="`/tematik/${tema.tema}`">{{ tema.name }}</NuxtLink>
              </td>
              <td class="py-3 px-5 text-center">{{ tema.national }}</td>
              <td class="py-3 px-5 text-center">10%</td>
              <td class="py-3 px-5 text-center">{{ tema.provincial }}</td>
              <td class="py-3 px-5 text-center">10%</td>
              <td class="py-3 px-5 text-center">{{ tema.district }}</td>
              <td class="py-3 px-5 text-center">5%</td>
            </tr>
            <tr class="border-t-[2px] font-semibold">
              <td colspan="3" class="py-3 px-5 text-center">Total</td>
              <td class="py-3 px-5 text-center">6.100.000.000,00</td>
              <td class="py-3 px-5"></td>
              <td class="py-3 px-5 text-center">7.500.000.000,00</td>
              <td class="py-3 px-5"></td>
              <td class="py-3 px-5 text-center">2.850.000.000,00</td>
              <td class="py-3 px-5"></td>
            </tr>
          </tbody>
        </table>

        <div class="flex justify-between mt-10 items-center">
          <h1 class="text-md font-medium">Data Update : 20 Juli 2024</h1>
          <nuxt-link to="">
            <button class="py-2 px-6 bg-[#009efb] rounded-lg text-white hover:scale-95 duration-150 transition-all">Terapkan</button>
          </nuxt-link>
        </div>
      </div>
    </div>
  </div>

  <TabsSystem />
</template>
