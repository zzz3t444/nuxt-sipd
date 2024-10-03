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

<template>
  <div v-if="!route.params.provinsi">
    <div class="flex justify-between items-center">
      <div class="">
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
      <div class="">
        <SelectYear />
      </div>
    </div>
    <div class="bg-white w-full sm:px-5 py-4 rounded-2xl my-8">
      <div class="w-full bg-white px-7 rounded-lg text-black py-8">
        <EntriesValue />
        <div class="w-full mt-10 overflow-x-auto">
          <table class="w-full">
            <thead>
              <tr>
                <th class="px-4">No</th>
                <th class="px-4">Tema</th>
                <th class="px-4">Anggaran / Provinsi</th>
                <th class="px-4">%{?}</th>
                <th class="px-4">Anggaran / Kabupaten</th>
                <!-- <th class="px-4">%{?}</th> -->
              </tr>
            </thead>
            <tbody>
              <tr class="border-t-[1px]" v-for="(prov, index) in provinsiList" :key="prov.id">
                <td class="py-3 px-5 text-center">{{ index + 1 }}</td>
                <td class="py-3 px-5">
                  <NuxtLink :to="`/tematik/${route.params.tema}/${prov.slug}`">
                    {{ prov.name }}
                  </NuxtLink>
                </td>
                <td class="py-3 px-5 text-center">{{ prov.anggaranP }}</td>
                <td class="py-3 px-5 text-center">10%</td>
                <td class="py-3 px-5 text-center">{{ prov.anggaranK }}</td>
                <!-- <td class="py-3 px-5 text-center">10%</td> -->
              </tr>
              <tr class="border-t-[2px] font-semibold">
                <td colspan="2" class="py-3 px-5 text-center">Total</td>
                <td class="py-3 px-5 text-center">230.000.000,00</td>
                <td class="py-3 px-5 text-center">10%</td>
                <td class="py-3 px-5 text-center">120.000.000,00</td>
                <!-- <td class="py-3 px-5 text-center">20%</td> -->
              </tr>
            </tbody>
          </table>
          <h1 class="text-md mt-10 font-medium">Data Update : 20 juli 2024</h1>
        </div>
      </div>
    </div>
    <!-- <div class="pt-8 flex justify-end">
      <Menu />
    </div> -->
    <div class="mt-5 w-full bg-white py-12 px-7 rounded-2xl text-white">
      <h1 class="text-start font-bold text-black text-2xl">Per Tingkatan Pemerintah Daerah</h1>
      <div class="grid justify-center items-center gap-3 py-12">
        <div class="flex items-center text-black gap-3 text-xl">
          <ul class="p-3 w-5 bg-[#ff9000]"></ul>
          <p>provinsi</p>
        </div>
        <div class="flex items-center text-black gap-3 text-xl">
          <ul class="p-3 w-5 bg-[#009efb]"></ul>
          <p>Kab/Kota</p>
        </div>
      </div>
      <div class="flex flex-col gap-8 w-full px-4">
        <ChartCollapse bgcolor="bg-[#ff9000]" title="Provinsi" ckey="1" />
        <ChartCollapse bgcolor="bg-[#009efb]" title="Kab / Kota" ckey="2" />
      </div>
    </div>
  </div>
  <NuxtPage v-else />
</template>
