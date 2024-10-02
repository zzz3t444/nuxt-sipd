<script setup>
const temaList = ref([
  { id: 1, name: "ANGKUTAN ORANG", tema: "ANGKUTAN ORANG" },
  { id: 2, name: "AUDITOR", tema: "AUDITOR" },
  { id: 3, name: "BENCANA", tema: "BENCANA" },
  { id: 4, name: "SIGA", tema: "SIGA" },
  { id: 5, name: "SERTIFIKASI", tema: "SERTIFIKASI" },
  { id: 6, name: "SISTEM MANAGEMENT", tema: "SISTEM MANAGEMENT" },
]);
</script>

<template>
  <div class="flex justify-between items-center">
    <div class="">
      <h1 class="text-2xl text-black">Tematik</h1>
      <h1 class="text-sm text-neutral-500">
        <NuxtLink to="/" class="text-[#009efb] hover:text-[#7460e]">Dashboard</NuxtLink>
        >
        <NuxtLink to="/" class="text-[#009efb] hover:text-[#7460e]">Informasi Pembangunan Daerah</NuxtLink>
        > Tematik
      </h1>
    </div>
    <div class="">
      <SelectYear />
    </div>
  </div>
  <div class="bg-white w-full sm:px-5 py-4 rounded-3xl my-8 text-white">
    <div class="w-full bg-white px-7 rounded-lg text-black py-8">
      <EntriesValue />
      <div class="w-full mt-10 overflow-x-auto">
        <table class="w-full">
          <thead>
            <th class="px-4">No</th>
            <th class="px-4">Tema</th>
            <th class="px-4">Nasional</th>
            <th class="px-4">%{?}</th>
            <th class="px-4">Provinsi</th>
            <th class="px-4">%{?}</th>
            <th class="px-4">Kab/Kota</th>
            <th class="px-4">%{?}</th>
          </thead>
          <tbody>
            <tr class="border-t-[1px]" v-for="(tema, index) in temaList">
              <td class="py-3 px-5 text-center">{{ index + 1 }}</td>
              <td class="py-3 px-5">
                <NuxtLink :to="`/tematik/${tema.tema}`">{{ tema.name }}</NuxtLink>
              </td>
              <td class="py-3 px-5 text-center">1.000.000.000,00</td>
              <td class="py-3 px-5 text-center">10%</td>
              <td class="py-3 px-5 text-center">2.000.000.000,00</td>
              <td class="py-3 px-5 text-center">10%</td>
            </tr>
            <tr class="border-t-[2px] font-semibold">
              <td colspan="2" class="py-3 px-5 text-center">Total</td>
              <td class="py-3 px-5 text-center">230.000.000,00</td>
              <td class="py-3 px-5"></td>
              <td class="py-3 px-5 text-center">120.000.000,00</td>
              <td class="py-3 px-5"></td>
              <td class="py-3 px-5 text-center">10.000.000</td>
              <td class="py-3 px-5"></td>
            </tr>
          </tbody>
        </table>
        <h1 class="text-md mt-10 font-medium">Data Update : 20 juli 2024</h1>
      </div>
    </div>
  </div>

  <TabsSystem />
</template>
