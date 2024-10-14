<script setup>
import { ref, computed } from "vue";
import { useRouter } from "vue-router";
import temaListData from "../../utils/TematikList.json";

const temaList = ref(temaListData);
const selectedRows = ref([]);
const selectedYear = ref("2024");
const selectedEntries = ref(25);
const years = [2025, 2024, 2023, 2022, 2021, 2020];
const currentPage = ref(1);

const filteredTemaList = computed(() => {
  return selectedYear.value === "2025" ? [] : temaList.value;
});

const totalPages = computed(() => {
  return Math.ceil(filteredTemaList.value.length / selectedEntries.value);
});

// New computed property to slice the filteredTemaList based on currentPage
const displayedTemaList = computed(() => {
  const start = (currentPage.value - 1) * selectedEntries.value;
  return filteredTemaList.value.slice(start, start + selectedEntries.value);
});

const updateYear = () => {
  console.log("Year updated to:", selectedYear.value);
  selectedRows.value = [];
  currentPage.value = 1; // Reset to first page
};

const router = useRouter();

const applySelection = () => {
  if (selectedRows.value.length > 0) {
    router.push({ name: "SelectedTemas", query: { selectedIds: selectedRows.value.join(",") } });
  } else {
    alert("Please select at least one item to apply.");
  }
};

// Navigation functions
const nextPage = () => {
  if (currentPage.value < totalPages.value) {
    currentPage.value++;
  }
};

const prevPage = () => {
  if (currentPage.value > 1) {
    currentPage.value--;
  }
};
</script>

<template>
  <div class="flex justify-between items-center">
    <div class="">
      <h1 class="text-2xl text-black">Bidang Urusan</h1>
      <h1 class="text-sm text-neutral-500">
        <NuxtLink to="/" class="text-[#009efb] hover:text-[#7460e]">Dashboard</NuxtLink>
        >
        <NuxtLink to="/" class="text-[#009efb] hover:text-[#7460e]">Informasi Pembangunan Daerah</NuxtLink>
        > Urusan Pemerintahan
      </h1>
    </div>
    <div class="">
      <SelectYear />
    </div>
  </div>

  <div class="bg-white w-full sm:px-5 py-4 rounded-2xl my-8 text-white">
    <div class="w-full bg-white px-7 rounded-lg text-black py-8">
      <div class="flex items-center gap-4">
        <span>Show</span>
        <select v-model="selectedEntries" class="py-2 px-3 w-[120px] outline-none rounded-md text-left bg-[#f2f7f8]">
          <option value="10">10</option>
          <option value="25">25</option>
          <option value="50">50</option>
          <option value="75">75</option>
          <option value="100">100</option>
        </select>
        <span>Entries</span>
        <span class="ml-16">Showing 0 to 0 of 0 entries</span>
      </div>

      <div class="w-full mt-10 overflow-x-auto">
        <table class="w-full" v-if="displayedTemaList.length > 0">
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
            <tr class="border-t-[1px]" v-for="(tema, index) in displayedTemaList" :key="tema.id">
              <td class="py-3 px-5 text-center">
                <input type="checkbox" :value="tema.id" v-model="selectedRows" />
              </td>
              <td class="py-3 px-5 text-center">{{ (currentPage.value - 1) * selectedEntries.value + index + 1 }}</td>
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

        <!-- Pagination Controls -->
        <div class="flex justify-between mt-5">
          <button @click="prevPage" :disabled="currentPage === 1" class="py-2 px-4 bg-blue-500 text-white rounded-lg">Previous</button>
          <span>Page {{ currentPage }} of {{ totalPages }}</span>
          <button @click="nextPage" :disabled="currentPage === totalPages" class="py-2 px-4 bg-blue-500 text-white rounded-lg">Next</button>
        </div>
        <div>
          <p class="text-lg mt-10 font-medium">Data Update : 12 Agustus 2024</p>
        </div>
      </div>
    </div>
  </div>
  <div>
    <TabsSystem />
  </div>
</template>
