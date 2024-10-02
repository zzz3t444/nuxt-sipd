<script setup>
defineProps({
  data: {
    type: Array,
    required: true,
  },
});
</script>

<template>
  <div class="overflow-auto">
    <div class="p-5">
      <table class="w-full border-collapse border border-gray-300">
        <thead>
          <tr class="grid grid-rows-2 grid-cols-8">
            <th class="row-span-2 col-span-1 border border-gray-300 p-2">No</th>
            <th class="row-span-2 col-span-1 border border-gray-300 p-2">Tahapan RKPD</th>
            <th class="row-span-1 col-span-2 border border-gray-300 p-2">Provinsi</th>
            <th class="row-span-1 col-span-2 border border-gray-300 p-2">Kabupaten</th>
            <th class="row-span-1 col-span-2 border border-gray-300 p-2">Kota</th>
            <th class="row-span-1 col-span-1 border border-gray-300 p-2">Input</th>
            <th class="row-span-1 col-span-1 border border-gray-300 p-2">Belum Input</th>
            <th class="row-span-1 col-span-1 border border-gray-300 p-2">Input</th>
            <th class="row-span-1 col-span-1 border border-gray-300 p-2">Belum Input</th>
            <th class="row-span-1 col-span-1 border border-gray-300 p-2">Input</th>
            <th class="row-span-1 col-span-1 border border-gray-300 p-2">Belum Input</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(item, index) in data" :key="index" class="grid grid-cols-8">
            <td class="border border-gray-300 p-2">{{ index + 1 }}</td>
            <td class="border border-gray-300 p-2">
              {{ item.tahapan_rkpd }}
            </td>
            <td class="border border-gray-300 p-2">
              {{ item.provinsi.input }}
            </td>
            <td class="border border-gray-300 p-2">
              {{ item.provinsi.belum_input }}
            </td>
            <td class="border border-gray-300 p-2">
              {{ item.kabupaten.input }}
            </td>
            <td class="border border-gray-300 p-2">
              {{ item.kabupaten.belum_input }}
            </td>
            <td class="border border-gray-300 p-2">
              {{ item.kota.input }}
            </td>
            <td class="border border-gray-300 p-2">
              {{ item.kota.belum_input }}
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>
