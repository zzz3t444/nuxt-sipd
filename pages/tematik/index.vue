<script setup>
import { ref, computed } from "vue";
import { useRouter } from "vue-router"; 
import temaListData from "../../utils/TematikList.json";

const temaList = ref(temaListData);
const selectedRows = ref([]);
const selectedYear = ref("2024");
const years = [2025, 2024, 2023, 2022, 2021, 2020];

const isAllSelected = computed(() => selectedRows.value.length === filteredTemaList.value.length && selectedRows.value.length > 0);

const toggleAll = () => {
  if (isAllSelected.value) {
    selectedRows.value = [];
  } else {
    selectedRows.value = filteredTemaList.value.map((item) => item.id);
  }
};

const filteredTemaList = computed(() => {
  return selectedYear.value === "2025" ? [] : temaList.value;
});

const updateYear = () => {
  console.log("Year updated to:", selectedYear.value);
  selectedRows.value = [];
};


const router = useRouter();
const applySelection = () => {
  if (selectedRows.value.length > 0) {

    router.push({ name: "SelectedTemas", params: { selectedIds: selectedRows.value } }); 
  } else {
    alert("Please select at least one item to apply.");
  }
};
</script>

<template>
  <div class="flex justify-between items-center">
    <div>
      <h1 class="text-2xl text-black">Tematik</h1>
      <h1 class="text-sm text-neutral-500">
        <NuxtLink to="/" class="text-[#009efb] hover:text-[#7460e]">Dashboard</NuxtLink>
        /
        <NuxtLink to="/" class="text-[#009efb] hover:text-[#7460e]">Informasi Pembangunan Daerah</NuxtLink>
        / Tematik
      </h1>
    </div>
    <div>
      <select v-model="selectedYear" @change="updateYear" name="tahun" id="tahun" class="bg-[#f20a34] rounded-full py-2 px-8 text-white font-semibold">
        <option v-for="year in years" :key="year" :value="year" class="bg-white text-black">Tahun {{ year }}</option>
      </select>
    </div>
  </div>

  <div class="bg-white w-full sm:px-5 py-4 rounded-2xl my-8 text-white">
    <div class="w-full bg-white px-7 rounded-lg text-black py-8">
      <EntriesValue />
      <div class="w-full mt-10 overflow-x-auto">
        <table class="w-full" v-if="filteredTemaList.length > 0">
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
            <tr class="border-t-[1px]" v-for="(tema, index) in filteredTemaList" :key="tema.id">
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
        <div v-else class="text-center text-gray-500 py-5">No data available for the selected year.</div>

        <div class="flex justify-between mt-10 items-center">
          <h1 class="text-md font-medium">Data Update : 20 Juli 2024</h1>
          <button @click="applySelection" class="py-2 px-6 bg-[#009efb] rounded-lg text-white hover:scale-95 duration-150 transition-all">Terapkan</button>
        </div>
      </div>
    </div>
  </div>

  <TabsSystem />
</template>
