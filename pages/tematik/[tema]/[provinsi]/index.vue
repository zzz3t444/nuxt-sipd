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
  <div class="bg-white w-full sm:px-14 py-4 rounded-lg my-8">
    <div class="w-full bg-white px-7 rounded-lg text-black py-8">
      <header class="flex items-center gap-10">
        <div class="flex items-center gap-4">
          <span>Show</span>
          <select name="entriescount" id="entriescount" class="py-2 px-3 w-[120px] outline-none text-black rounded-md text-left bg-[#f2f7f8]">
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
            <th class="px-4">Anggaran / Nasional</th>
            <th class="px-4">%{?}</th>
            <th class="px-4">Anggaran / Provinsi</th>
            <th class="px-4">%{?}</th>
          </thead>
          <tbody>
            <tr class="border-t-2" v-for="(kabupaten, index) in kabupatenList">
              <td class="py-4 px-5 text-center">{{ index + 1 }}</td>
              <td class="py-4 px-5">
                <NuxtLink>{{ kabupaten.name }}</NuxtLink>
              </td>
              <td class="py-4 px-5 text-center">1.000.000.000,00</td>
              <td class="py-4 px-5 text-center">10%</td>
              <td class="py-4 px-5 text-center">2.000.000.000,00</td>
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
    <h1 class="text-center font-bold text-2xl">Proporsi Pendanaan Per Tingkatan Pemerintah Daerah</h1>
    <div class="flex justify-center items-center gap-24 py-12">
      <span class="px-10 py-2 bg-sky-500">PROV</span>
      <span class="px-10 py-2 bg-yellow-500">KABKOT</span>
    </div>
    <div class="flex flex-col gap-8 w-full px-4">
      <ChartCollapse bgcolor="bg-sky-500" title="Provinsi" ckey="1" />
      <ChartCollapse bgcolor="bg-yellow-500" title="Kab / Kota" ckey="2" />
    </div>
  </div>
</template>

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
