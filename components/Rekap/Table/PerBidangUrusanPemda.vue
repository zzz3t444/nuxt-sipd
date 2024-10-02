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
      item.kode_pemda.toLowerCase().includes(searchTerm.value.toLowerCase()) ||
      item.pemda.toLowerCase().includes(searchTerm.value.toLowerCase()) ||
      item.kode_bidang.toLowerCase().includes(searchTerm.value.toLowerCase()) ||
      item.bidang_urusan.toLowerCase().includes(searchTerm.value.toLowerCase())
  );
});
</script>

<template>
  <div class="overflow-auto">
    <div class="p-5">
      <input v-model="searchTerm" type="text" placeholder="Search by name, code, or bidang urusan" class="mb-2 p-2 border border-gray-300 rounded" />
      <table class="w-full border-collapse border border-gray-300">
        <thead>
          <tr class="">
            <th class="border border-gray-300 p-2">No</th>
            <th class="border border-gray-300 p-2">Kode Pemda</th>
            <th class="border border-gray-300 p-2">Pemda</th>
            <th class="border border-gray-300 p-2">Kode Bidang</th>
            <th class="border border-gray-300 p-2">Bidang Urusan</th>
            <th class="border border-gray-300 p-2">Jumlah Program</th>
            <th class="border border-gray-300 p-2">Jumlah Kegiatan</th>
            <th class="border border-gray-300 p-2">Jumlah Sub Kegiatan</th>
            <th class="border border-gray-300 p-2">Pagu</th>
            <th class="border border-gray-300 p-2">%</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(item, index) in filteredData" :key="index">
            <td class="border border-gray-300 p-2">{{ index + 1 }}</td>
            <td class="border border-gray-300 p-2">
              {{ item.kode_pemda }}
            </td>
            <td class="border border-gray-300 p-2">{{ item.pemda }}</td>
            <td class="border border-gray-300 p-2">
              {{ item.kode_bidang }}
            </td>
            <td class="border border-gray-300 p-2">
              {{ item.bidang_urusan }}
            </td>
            <td class="border border-gray-300 p-2">
              {{ item.jumlah_program }}
            </td>
            <td class="border border-gray-300 p-2">
              {{ item.jumlah_kegiatan }}
            </td>
            <td class="border border-gray-300 p-2">
              {{ item.jumlah_sub_kegiatan }}
            </td>
            <td class="border border-gray-300 p-2">
              {{ item.pagu }}
            </td>
            <td class="border border-gray-300 p-2">
              {{ item.persen }}
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>
