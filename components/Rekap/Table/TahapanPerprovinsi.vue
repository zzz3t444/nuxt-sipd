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
      item.tahapan_akhir_di_sipd.toLowerCase().includes(searchTerm.value.toLowerCase()) ||
      item.nama_tahapan.toLowerCase().includes(searchTerm.value.toLowerCase())
  );
});
</script>

<template>
  <div class="overflow-auto">
    <div class="">
      <table class="w-full border-collapse border border-gray-300">
        <thead>
          <tr>
            <th class="border border-gray-300 p-2">No</th>
            <th class="border border-gray-300 p-2">Provinsi</th>
            <th class="border border-gray-300 p-2">Kode</th>
            <th class="border border-gray-300 p-2">Tahapan Akhir di SIPD</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(item, index) in filteredData" :key="index">
            <td class="border border-gray-300 p-2">{{ index + 1 }}</td>
            <td class="border border-gray-300 p-2">
              {{ item.nama_daerah }}
            </td>
            <td class="border border-gray-300 p-2">
              {{ item.kode_pemda }}
            </td>
            <td class="border border-gray-300 p-2">
              <h1>
                {{ item.tahapan_akhir_di_sipd }} -
                {{ item.nama_tahapan }}
              </h1>
              <h1 class="w-fit bg-[#f62d51] text-white text-sm p-1 rounded">Tanggal: {{ item.tanggal || "-" }}</h1>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>
