<script>
export default {
  data() {
    return {
      activeTable: "table1", // Default ke Table 1
    };
  },
};
</script>

<template>
  <div>
    <div class="flex flex-row table-selector w-full mt-10">
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
      <div
        @click="activeTable = 'table2'"
        :class="{
          'text-white bg-[#009efb] rounded-tl-xl rounded-tr-xl': activeTable === 'table2',
          'text-[#069aff]': activeTable !== 'table2',
        }"
        class="flex flex-row items-center p-3 gap-3 cursor-pointer">
        <div v-if="activeTable === 'table2'" class="text-xl">
          <i class="h-full fa-solid fa-chevron-right font-bold"></i>
        </div>
        Pagu Per SKPD
      </div>
    </div>
    <div class="p-5 w-full bg-white">
      <div v-if="activeTable === 'table1'" class="">
        <table class="w-full border-collapse border border-[#E8EEF3]">
          <thead>
            <tr class="grid grid-rows-2 grid-cols-4 bg-[#263238] text-white">
              <th class="row-span-2 col-span-1 border border-[#E8EEF3] p-2 flex justify-center items-center">Kode</th>
              <th class="row-span-2 col-span-1 border border-[#E8EEF3] p-2 flex justify-center items-center">Urai Bidang</th>
              <th class="row-span-1 col-span-2 border border-[#E8EEF3] p-2 text-center">Pagu</th>
              <th class="row-span-1 col-span-1 border border-[#E8EEF3] p-2 text-center">Total</th>
              <th class="row-span-1 col-span-1 border border-[#E8EEF3] p-2 text-center">Persen</th>
            </tr>
          </thead>

          <tbody>
            <tr class="grid grid-cols-4">
              <td class="border border-[#E8EEF3] p-2">1</td>
              <td class="border border-[#E8EEF3] p-2">2</td>
              <td class="border border-[#E8EEF3] p-2">3</td>
              <td class="border border-[#E8EEF3] p-2">4</td>
            </tr>
          </tbody>
        </table>
      </div>

      <div v-else class="">
        <table class="w-full border-collapse border border-[#E8EEF3]">
          <thead>
            <tr class="grid grid-rows-2 grid-cols-4">
              <th class="row-span-2 col-span-1 border border-[#E8EEF3] p-2">kode</th>
              <th class="row-span-2 col-span-1 border border-[#E8EEF3] p-2">SKPD</th>
              <th class="row-span-1 col-span-2 border border-[#E8EEF3] p-2">Pagu</th>
              <th class="row-span-1 col-span-1 border border-[#E8EEF3] p-2">Total</th>
              <th class="row-span-1 col-span-1 border border-[#E8EEF3] p-2">Persen</th>
            </tr>
          </thead>
          <tbody>
            <tr class="grid grid-cols-4">
              <td class="border border-[#E8EEF3] p-2">1</td>
              <td class="border border-[#E8EEF3] p-2">2</td>
              <td class="border border-[#E8EEF3] p-2">3</td>
              <td class="border border-[#E8EEF3] p-2">4</td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>
