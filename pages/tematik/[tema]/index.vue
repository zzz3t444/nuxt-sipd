<script setup>
import { ref, computed } from "vue";
import { useRoute } from "vue-router";
import provinsiListData from "@/utils/provinsilist.json";
import provincesData from "@/utils/provinceName.json";

const route = useRoute();
const provinsiList = ref(provinsiListData);
const provinces = ref(provincesData);
const entriesCount = ref(10);
const openDropdown = ref(null); 

const filteredProvinsiList = computed(() => {
  return provinsiList.value.slice(0, entriesCount.value);
});

const toggleDropdown = (prov) => {

  if (openDropdown.value && openDropdown.value !== prov) {
    openDropdown.value.showDropdown = false;
  }

  // Toggle the clicked dropdown
  prov.showDropdown = !prov.showDropdown;

  // Update the openDropdown reference
  openDropdown.value = prov.showDropdown ? prov : null;
};

const toggleCheckbox = (province, prov) => {
  province.checked = !province.checked;

  if (province.checked) {
    if (!prov.selectedProvinces.includes(province.name)) {
      prov.selectedProvinces.push(province.name);
    }

    province.districts.forEach((district) => {
      district.checked = true;
      if (!prov.selectedDistricts.includes(district.name)) {
        prov.selectedDistricts.push(district.name);
      }
    });
  } else {
    prov.selectedProvinces = prov.selectedProvinces.filter((name) => name !== province.name);

    province.districts.forEach((district) => {
      district.checked = false;
      prov.selectedDistricts = prov.selectedDistricts.filter((name) => name !== district.name);
    });
  }

  prov.selectAll = provinces.value.every((p) => p.checked);
};

const toggleSelectAll = (prov) => {
  prov.selectAll = !prov.selectAll;
  provinces.value.forEach((province) => {
    province.checked = prov.selectAll;
    if (prov.selectAll) {
      if (!prov.selectedProvinces.includes(province.name)) {
        prov.selectedProvinces.push(province.name);
      }

      province.districts.forEach((district) => {
        district.checked = true;
        if (!prov.selectedDistricts.includes(district.name)) {
          prov.selectedDistricts.push(district.name);
        }
      });
    } else {
      prov.selectedProvinces = [];

      province.districts.forEach((district) => {
        district.checked = false;
        prov.selectedDistricts = [];
      });
    }
  });
};
</script>

<template>
  <div v-if="!route.params.provinsi">
    <div class="flex justify-between items-center">
      <div>
        <h1 class="text-2xl text-black">Tematik</h1>
        <h1 class="text-sm text-neutral-500">
          <NuxtLink to="/" class="text-[#009efb] hover:text-[#7460e]">Dashboard</NuxtLink>
          /
          <NuxtLink to="/" class="text-[#009efb] hover:text-[#7460e]">Informasi Pembangunan Daerah</NuxtLink>
          /
          <NuxtLink to="/tematik" class="text-[#009efb] hover:text-[#7460e]">Tematik</NuxtLink>
          / {{ route.params.tema }}
        </h1>
      </div>
      <div>
        <SelectYear />
      </div>
    </div>
    <div class="bg-white w-full sm:px-5 py-4 rounded-2xl my-8">
      <div class="w-full bg-white px-7 rounded-lg text-black py-8">
        <header class="flex items-center mb-5 gap-10">
          <div class="flex items-center gap-4">
            <span>Show</span>
            <select name="entriescount" id="entriescount" class="py-2 px-3 w-[120px] outline-none rounded-md text-left bg-[#f2f7f8]" v-model="entriesCount">
              <option value="10">10</option>
              <option value="25">25</option>
              <option value="50">50</option>
              <option value="100">100</option>
            </select>
            <span>Entries</span>
          </div>
          <div>
            <span>Showing 0 to {{ filteredProvinsiList.length }} of {{ provinsiList.length }} entries</span>
          </div>
        </header>
        <div class="w-full mt-10 overflow-x-auto">
          <table class="w-full">
            <thead>
              <tr>
                <th class="px-4">No</th>
                <th class="px-4">Tema</th>
                <th class="px-4">Anggaran / Provinsi</th>
                <th class="px-4">%{?}</th>
                <th class="px-4">Anggaran / Kabupaten</th>
              </tr>
            </thead>
            <tbody>
              <tr class="border-t-[1px]" v-for="(prov, index) in filteredProvinsiList" :key="prov.id">
                <td class="py-3 px-5 text-center">{{ index + 1 }}</td>
                <td class="py-3 px-5">{{ prov.name }}</td>
                <td class="py-3 px-5 text-center">
                  <button @click="toggleDropdown(prov)" class="text-blue-500">
                    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="2" stroke="currentColor" class="w-4 h-4 inline">
                      <path stroke-linecap="round" stroke-linejoin="round" d="M19 9l-7 7-7-7" />
                    </svg>
                  </button>

                  {{ prov.anggaranP }}

                  <div v-if="prov.showDropdown" class="absolute bg-white border border-gray-300 shadow-lg mt-2 w-96 max-h-80 p-4 rounded-lg overflow-y-auto">
                    <ul>
                      <li class="flex items-center p-2 hover:bg-gray-100">
                        <input type="checkbox" :checked="prov.selectAll" @change="toggleSelectAll(prov)" />
                        <span class="ml-2">Select All</span>
                      </li>
                      <li v-for="province in provinces" :key="province.id" class="flex items-start p-2 hover:bg-gray-100">
                        <input type="checkbox" v-model="province.checked" @change="toggleCheckbox(province, prov)" />
                        <span class="ml-2">{{ province.name }}</span>

                        <button @click="province.showDistricts = !province.showDistricts" class="ml-2 text-blue-500">
                          <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="2" stroke="currentColor" class="w-4 h-4 inline">
                            <path stroke-linecap="round" stroke-linejoin="round" d="M19 9l-7 7-7-7" />
                          </svg>
                        </button>

                        <div v-if="province.showDistricts" class="ml-4 bg-gray-100 p-2 rounded">
                          <ul>
                            <li v-for="district in province.districts" :key="district.name" class="flex items-center p-2 hover:bg-gray-200">
                              <input type="checkbox" v-model="district.checked" />
                              <span class="ml-2">{{ district.name }}</span>
                            </li>
                          </ul>
                        </div>
                      </li>
                    </ul>
                  </div>

                  <div v-if="prov.selectedProvinces.length" class="mt-1 text-sm text-gray-600">{{ prov.selectedProvinces.length }} selected</div>
                </td>
                <td class="py-3 px-5 text-center">10%</td>
                <td class="py-3 px-5 text-center">{{ prov.anggaranK }}</td>
              </tr>
              <tr class="border-t-[2px] font-semibold">
                <td colspan="2" class="py-3 px-5 text-center">Total</td>
                <td class="py-3 px-5 text-center">230.000.000,00</td>
                <td class="py-3 px-5 text-center">10%</td>
                <td class="py-3 px-5 text-center">120.000.000,00</td>
              </tr>
            </tbody>
          </table>
          <div class="flex items-center justify-between p-10 pb-0">
            <h1 class="text-md font-medium">Data Update : 20 Juli 2024</h1>
            <nuxt-link to="">
              <button class="py-2 px-6 bg-[#009efb] rounded-lg text-white hover:scale-95 duration-150 transition-all">Terapkan</button>
            </nuxt-link>
          </div>
        </div>
      </div>
    </div>
    <TabsSystem />
  </div>
  <NuxtPage v-else />
</template>

<style scoped>
.absolute {
  position: absolute;
}

.max-h-80 {
  max-height: 30rem;
}

.w-96 {
  width: 44rem;
}

.p-4 {
  padding: 1rem;
}
</style>
