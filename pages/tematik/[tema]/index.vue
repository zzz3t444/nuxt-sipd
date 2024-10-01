<template>
  <div v-if="!route.params.provinsi">
    <div class="flex justify-between items-center">
      <div class="">
        <h1 class="text-2xl text-white">Tematik</h1>
        <h1 class="text-sm text-white">
          <NuxtLink to="/" class="text-[#009efb] hover:text-[#7460e]"
            >Dashboard</NuxtLink
          >
          >
          <NuxtLink to="/" class="text-[#009efb] hover:text-[#7460e]"
            >Informasi Pembangunan Daerah</NuxtLink
          >
          >
          <NuxtLink to="/tematik" class="text-[#009efb] hover:text-[#7460e]"
            >Tematik</NuxtLink
          >
          > {{ route.params.tema }}
        </h1>
      </div>
      <div class="">
        <SelectYear />
      </div>
    </div>
    <div class="bg-white w-full sm:px-14 py-4 rounded-lg my-8 ">
      <div class="w-full bg-white px-7 rounded-lg text-black py-8">
        <header class="flex items-center gap-10">
          <div class="flex items-center gap-4">
            <span>Show</span>
            <select
              name="entriescount"
              id="entriescount"
              class="py-2 px-3 w-[120px] outline-none rounded-md text-left text-black bg-[#f2f7f8]"
            >
              <option value="10">10</option>
              <option value="10">25</option>
              <option value="50">50</option>
              <option value="50">75</option>
              <option value="100" selected>100</option>
            </select>
            <span>Entries</span>
          </div>
          <div class="">
            <span>Showing 0 to 0 of 0 entries</span>
          </div>
        </header>
        <div class="w-full mt-5 overflow-x-auto">
          <table class="w-full">
            <thead>
              <th class="px-4">No</th>
              <th class="px-4">Tema</th>
              <th class="px-4">Anggaran / Provinsi</th>
              <th class="px-4">%{?}</th>
              <th class="px-4">Anggaran / Kabupaten</th>
              <th class="px-4">%{?}</th>
            </thead>
            <tbody>
              <tr
                class="border-t-2"
                v-for="(prov, index) in provinsiList"
                :key="prov.id"
              >
                <td class="py-4 px-5 text-center">{{ index + 1 }}</td>
                <td class="py-4 px-5">
                  <NuxtLink :to="`/tematik/${route.params.tema}/${prov.slug}`">
                    {{ prov.name }}
                  </NuxtLink>
                </td>
                <td class="py-4 px-5 text-center">{{ prov.anggaranP }}</td>
                <td class="py-4 px-5 text-center">10%</td>
                <td class="py-4 px-5 text-center">{{ prov.anggaranK }}</td>
                <td class="py-4 px-5 text-center">10%</td>
              </tr>
            </tbody>
          </table>
        </div>
        <footer>
          <div class="flex justify-between mt-10 items-center">
            <span class="font-bold text-xl"> Total: </span>
            <span class="font-bold">5.000.000.000,00</span>
            <div class="w-[70px]"></div>
          </div>
          <div class="text-lg mt-4">Data Update : 20 Juli 2024</div>
        </footer>
      </div>
    </div>
    <div class="pt-8 flex justify-end">
      <Menu />
    </div>
    <div class="mt-5 w-full bg-[#272B34] py-12 px-7 rounded-lg text-white">
      <h1 class="text-center font-bold text-2xl">
        Proporsi Pendanaan Per Tingkatan Pemerintah Daerah
      </h1>
      <div class="flex justify-center items-center gap-24 py-12">
        <span class="px-10 py-2 bg-sky-500">PROV</span>
        <span class="px-10 py-2 bg-yellow-500">KABKOT</span>
      </div>
      <div class="flex flex-col gap-8 w-full px-4">
        <ChartCollapse bgcolor="bg-sky-500" title="Provinsi" ckey="1" />
        <ChartCollapse bgcolor="bg-yellow-500" title="Kab / Kota" ckey="2" />
      </div>
    </div>
  </div>
  <NuxtPage v-else />
</template>

<script setup>
const route = useRoute();

const provinsiList = ref([
  {
    id: 1,
    name: "Aceh",
    slug: "aceh",
    anggaranP: "Rp 1.000.000.000",
    anggaranK: "Rp 2.000.000.000",
  },
  {
    id: 2,
    name: "Sumatera Utara",
    slug: "sumut",
    anggaranP: "Rp 1.500.000.000",
    anggaranK: "Rp 2.500.000.000",
  },
]);
</script>
