<script setup>
const route = useRoute();

const kabupatenList = ref([]);

const getKabupatenList = (provinsi) => {
  if (provinsi === "aceh") {
    return [
      { id: 1, name: "Kabupaten Aceh Besar", anggaran: "Rp 300.000.000" },
      { id: 2, name: "Kabupaten Pidie", anggaran: "Rp 250.000.000" },
    ];
  } else if (provinsi === "sumut") {
    return [
      { id: 1, name: "Kabupaten Deli Serdang", anggaran: "Rp 400.000.000" },
      { id: 2, name: "Kabupaten Langkat", anggaran: "Rp 350.000.000" },
    ];
  }
  return [];
};

onMounted(() => {
  kabupatenList.value = getKabupatenList(route.params.provinsi);
});

watch(
  () => route.params.provinsi,
  (newProvinsi) => {
    kabupatenList.value = getKabupatenList(newProvinsi);
  }
);
</script>

<template>
  <div class="flex justify-between items-center">
    <div class="">
      <h1 class="text-2xl text-black">Tematik</h1>
      <h1 class="text-sm text-neutral-500">
        <NuxtLink to="/" class="text-[#009efb] hover:text-[#7460e]">Dashboard</NuxtLink>
        >
        <NuxtLink to="/" class="text-[#009efb] hover:text-[#7460e]">Informasi Pembangunan Daerah</NuxtLink>
        >
        <NuxtLink to="/tematik" class="text-[#009efb] hover:text-[#7460e]">Tematik</NuxtLink>
        >
        <NuxtLink :to="`/tematik/${route.params.tema}`" class="text-[#009efb] hover:text-[#7460e]">
          {{ route.params.tema }}
        </NuxtLink>
        >
        {{ route.params.provinsi }}
      </h1>
    </div>
    <div class="">
      <SelectYear />
    </div>
  </div>

  <div class="bg-white w-full sm:px-5 py-4 rounded-lg my-8">
    <div class="w-full bg-white px-7 rounded-lg text-black py-8">
      <EntriesValue />
      <div class="w-full mt-10 overflow-x-auto">
        <table class="w-full">
          <thead>
            <tr>
              <th class="px-4">No</th>
              <th class="px-4">Tema</th>
              <th class="px-4">Anggaran / Nasional</th>
              <th class="px-4">% Nasional</th>
              <th class="px-4">Anggaran / Provinsi</th>
              <th class="px-4">% Provinsi</th>
            </tr>
          </thead>
          <tbody>
            <tr class="border-t-[1px]" v-for="(kabupaten, index) in kabupatenList" :key="index">
              <td class="py-3 px-5 text-center">{{ index + 1 }}</td>
              <td class="py-3 px-5">
                <NuxtLink>{{ kabupaten.name }}</NuxtLink>
              </td>
              <td class="py-3 px-5 text-center">1.000.000.000,00</td>
              <td class="py-3 px-5 text-center">10%</td>
              <td class="py-3 px-5 text-center">2.000.000.000,00</td>
              <td class="py-3 px-5 text-center">10%</td>
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
        <h1 class="text-md mt-10 font-medium">Data Update : 21 juli 2024</h1>
      </footer>
    </div>
  </div>

  <!-- <div class="pt-8 flex justify-end">
    <Menu />
  </div> -->
  <div class="mt-5 w-full bg-white py-12 px-7 rounded-lg text-white">
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
</template>
