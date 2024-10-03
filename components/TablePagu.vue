<script setup>
import { ref } from "vue";

const activeTable = ref("table1"); // Default to "table1"
</script>

<template>
  <div>
    <!-- Table Selector Tabs -->
    <div class="flex flex-row table-selector w-full mt-10">
      <!-- First Tab: Pagu Per Bidang Urusan -->
      <div
        @click="activeTable = 'table1'"
        :class="{
          'text-white bg-[#009efb] rounded-tl-xl rounded-tr-xl': activeTable === 'table1',
          'text-[#069aff]': activeTable !== 'table1',
        }"
        class="flex flex-row items-center p-3 gap-3 cursor-pointer">
        <div v-if="activeTable === 'table1'" class="text-xl font-bold">
          <i class="h-full fa-solid fa-chevron-right"></i>
        </div>
        Pagu Per Bidang Urusan
      </div>

      <!-- Second Tab: Pagu Per SKPD -->
      <div
        @click="activeTable = 'table2'"
        :class="{
          'text-white bg-[#009efb] rounded-tl-xl rounded-tr-xl': activeTable === 'table2',
          'text-[#069aff]': activeTable !== 'table2',
        }"
        class="flex flex-row items-center p-3 gap-3 cursor-pointer">
        <div v-if="activeTable === 'table2'" class="text-xl font-bold">
          <i class="h-full fa-solid fa-chevron-right"></i>
        </div>
        Pagu Per SKPD
      </div>
    </div>

    <!-- Table Content -->
    <div class="p-5 w-full bg-white">
      <div v-if="activeTable === 'table1'" class="overflow-x-auto">
        <table class="w-full border-collapse border border-[#E8EEF3]">
          <thead>
            <tr class="bg-white text-black">
              <th class="border border-[#E8EEF3] p-2 text-center">Kode</th>
              <th class="border border-[#E8EEF3] p-2 text-left">Urai Bidang</th>
              <th class="border border-[#E8EEF3] p-2 text-center">Total</th>
              <th class="border border-[#E8EEF3] p-2 text-center">Persen</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td class="border border-[#E8EEF3] p-2 text-center">1.01</td>
              <td class="border border-[#E8EEF3] p-2 text-left text-[#069aff] font-semibold">
                URUSAN PEMERINTAHAN BIDANG PENDIDIKAN
                <div class="text-sm text-green-500">Jumlah SKPD: 5</div>
              </td>
              <td class="border border-[#E8EEF3] p-2 text-center">3.570.751.683.249,00</td>
              <td class="border border-[#E8EEF3] p-2 text-center">5.87</td>
            </tr>
            <tr>
              <td class="border border-[#E8EEF3] p-2 text-center">1.03</td>
              <td class="border border-[#E8EEF3] p-2 text-left text-[#069aff] font-semibold">
                URUSAN PEMERINTAHAN BIDANG PEKERJAAN UMUM DAN PENATAAN RUANG
                <div class="text-sm text-green-500">Jumlah SKPD: 5</div>
              </td>
              <td class="border border-[#E8EEF3] p-2 text-center">7.508.752.031.699,00</td>
              <td class="border border-[#E8EEF3] p-2 text-center">6.15</td>
            </tr>
            <!-- Add more rows here as needed -->
          </tbody>
        </table>
      </div>

      <!-- Table for Pagu Per SKPD -->
      <div v-if="activeTable === 'table2'" class="overflow-x-auto">
        <table class="w-full border-collapse border border-[#E8EEF3]">
          <thead>
            <tr class="bg-white text-black">
              <th class="border border-[#E8EEF3] p-2 text-center">Kode</th>
              <th class="border border-[#E8EEF3] p-2 text-left">SKPD</th>
              <th class="border border-[#E8EEF3] p-2 text-center">Total</th>
              <th class="border border-[#E8EEF3] p-2 text-center">Persen</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td class="border border-[#E8EEF3] p-2 text-center">1.01</td>
              <td class="border border-[#E8EEF3] p-2 text-left text-[#069aff] font-semibold">
                DINAS PENDIDIKAN
                <div class="text-sm text-green-500">Bidang Pendidikan</div>
              </td>
              <td class="border border-[#E8EEF3] p-2 text-center">3.570.751.683.249,00</td>
              <td class="border border-[#E8EEF3] p-2 text-center">5.87</td>
            </tr>
            <tr>
              <td class="border border-[#E8EEF3] p-2 text-center">1.02</td>
              <td class="border border-[#E8EEF3] p-2 text-left text-[#069aff] font-semibold">
                DINAS PEKERJAAN UMUM
                <div class="text-sm text-green-500">Bidang Pekerjaan Umum</div>
              </td>
              <td class="border border-[#E8EEF3] p-2 text-center">7.508.752.031.699,00</td>
              <td class="border border-[#E8EEF3] p-2 text-center">6.15</td>
            </tr>
            <!-- Add more rows as needed -->
          </tbody>
        </table>
      </div>

      <!-- Data Update Information -->
      <div class="flex justify-between mt-5 items-center">
        <h1 class="text-md font-medium">Data Update: 12 Agustus 2020</h1>
        <!-- <button class="py-2 px-6 bg-[#009efb] rounded-lg text-white hover:scale-95 transition duration-150">Terapkan</button> -->
      </div>
    </div>
  </div>
</template>

<style scoped>
.table-selector div {
  transition: all 0.2s;
}
</style>
