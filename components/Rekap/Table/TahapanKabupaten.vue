<template>
  <div class="overflow-auto">
    <div class="p-5">
      <input
        v-model="searchTerm"
        type="text"
        placeholder="Search by name, code, or bidang urusan"
        class="mb-2 p-2 border border-gray-300 rounded"
      />
      <table class="w-full border-collapse border border-gray-300">
        <thead>
          <tr class="grid grid-rows-2 grid-cols-12">
            <th class="row-span-2 col-span-1 border border-gray-300 p-2">
              Kode
            </th>
            <th class="row-span-2 col-span-1 border border-gray-300 p-2">
              Provinsi
            </th>
            <th class="row-span-1 col-span-10 border border-gray-300 p-2">
              Jumlah Rekap Tahapan di Kab/Kota Per-Provinsi
            </th>
            <th class="row-span-1 col-span-1 border border-gray-300 p-2">
              Belum Input
            </th>
            <th class="row-span-1 col-span-1 border border-gray-300 p-2">
              Rancangan Awal
            </th>
            <th class="row-span-1 col-span-1 border border-gray-300 p-2">
              Rancangan
            </th>
            <th class="row-span-1 col-span-1 border border-gray-300 p-2">
              Musrenbang
            </th>
            <th class="row-span-1 col-span-1 border border-gray-300 p-2">
              Rancangan Akhir
            </th>
            <th class="row-span-1 col-span-1 border border-gray-300 p-2">
              Penetapan
            </th>
            <th class="row-span-1 col-span-1 border border-gray-300 p-2">
              Rancangan KUA dan PPAS
            </th>
            <th class="row-span-1 col-span-1 border border-gray-300 p-2">
              Penetapan KUA dan PPAS
            </th>
            <th class="row-span-1 col-span-1 border border-gray-300 p-2">
              Rancangan APBD
            </th>
            <th class="row-span-1 col-span-1 border border-gray-300 p-2">
              Penetapan APBD
            </th>
          </tr>
        </thead>
        <tbody>
          <tr
            v-for="(item, index) in filteredData"
            :key="index"
            class="grid grid-cols-12"
          >
            <td class="border border-gray-300 p-2">
              {{ item.kode_pemda }}
            </td>
            <td class="border border-gray-300 p-2">
              {{ item.nama_daerah }}
            </td>
            <td class="border border-gray-300 p-2">
              <span class=" ">
                {{ item.tahapan.belum_input }}
              </span>
            </td>
            <td class="border border-gray-300 p-2">
              <span class=" "> {{ item.tahapan.rancangan_awal }}</span>
            </td>
            <td class="border border-gray-300 p-2">
              <span class=" "> {{ item.tahapan.rancangan }}</span>
            </td>
            <td class="border border-gray-300 p-2">
              <span class=" "> {{ item.tahapan.musrenbang }}</span>
            </td>
            <td class="border border-gray-300 p-2">
              <span class=" "> {{ item.tahapan.rancangan_akhir }}</span>
            </td>
            <td class="border border-gray-300 p-2">
              <span class=" "> {{ item.tahapan.penetapan }}</span>
            </td>
            <td class="border border-gray-300 p-2">
              <span class=" "> {{ item.tahapan.rancangan_kua_dan_ppas }}</span>
            </td>
            <td class="border border-gray-300 p-2">
              <span class=" "> {{ item.tahapan.penetapan_kua_dan_ppas }}</span>
            </td>
            <td class="border border-gray-300 p-2">
              <span class=" "> {{ item.tahapan.rancangan_apbd }}</span>
            </td>
            <td class="border border-gray-300 p-2">
              <span class=" "> {{ item.tahapan.penetapan_apbd }}</span>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script setup>
const props = defineProps({
  data: {
    type: Array,
    required: true,
  },
});

const searchTerm = ref("");

const filteredData = computed(() => {
  if (!searchTerm.value) return props.data;
  return props.data.filter(
    (item) =>
      item.nama_daerah.toLowerCase().includes(searchTerm.value.toLowerCase()) ||
      item.kode_pemda.includes(searchTerm.value) ||
      item.tahapan.belum_input.toString().includes(searchTerm.value) ||
      item.tahapan.musrenbang.toString().includes(searchTerm.value) ||
      item.tahapan.penetapan.toString().includes(searchTerm.value) ||
      item.tahapan.penetapan_apbd.toString().includes(searchTerm.value) ||
      item.tahapan.penetapan_kua_dan_ppas
        .toString()
        .includes(searchTerm.value) ||
      item.tahapan.rancangan.toString().includes(searchTerm.value) ||
      item.tahapan.rancangan_apbd.toString().includes(searchTerm.value) ||
      item.tahapan.rancangan_kua_dan_ppas
        .toString()
        .includes(searchTerm.value) ||
      item.tahapan.rancangan_akhir.toString().includes(searchTerm.value) ||
      item.tahapan.rancangan_awal.toString().includes(searchTerm.value)
  );
});
</script>
