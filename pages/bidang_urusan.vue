<script setup>
const temaList = ["Air minum", "Perhutanan Sosial", "Stunting", "Infrastruktur", "Sumberdana DAK (Sekretariat)"];

const subKegiatan = {
  provinsi: ["kegiatan provinsi 1", "kegiatan provinsi 2", "kegiatan provinsi 3", "kegiatan provinsi 4", "kegiatan provinsi 5"],
  "kab/kota": ["kegiatan kab/kota 1", "kegiatan kab/kota 2", "kegiatan kab/kota 3", "kegiatan kab/kota 4", "kegiatan kab/kota 5"],
};

const lingkup = ["nasional", "provinsi", "kab/kota"];
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

  <div class="bg-white w-full px-4 sm:px-20 py-10 rounded-3xl my-8">
    <form class="flex flex-col gap-3 w-full">
      <!-- First Row -->
      <div class="flex flex-col md:flex-row items-center gap-5">
        <div class="flex flex-col gap-2 w-full md:w-[50%]">
          <label for="tema" class="text-black">Pilih Tema</label>
          <SelectInput :render="temaList" class="w-full" selectname="tema" selectid="tema" />
        </div>
        <div class="flex flex-col gap-2 w-full md:w-[50%]">
          <label for="subkegiatan" class="text-black">Pilih Sub kegiatan</label>
          <MultipleSelectInput :render="subKegiatan" class="w-full" selectname="subkegiatan" selectid="subkegiatan" />
        </div>
      </div>

      <!-- <div class="flex flex-col gap-2">
        <label for="lingkup" class="text-black">Lingkup</label>
        <SelectInput :render="lingkup" class="w-full" selectname="lingkup" selectid="lingkup" />
      </div> -->

      <!-- Third Row -->
      <div class="flex flex-col md:flex-row items-center gap-5">
        <div class="flex flex-col gap-2 w-full md:w-[50%]">
          <label for="provinsi" class="text-black">Provinsi</label>
          <SelectInput :render="temaList" class="w-full" selectname="provinsi" selectid="provinsi" />
        </div>
        <div class="flex flex-col gap-2 w-full md:w-[50%]">
          <label for="kota" class="text-black">Kab / Kota</label>
          <SelectInput :render="temaList" class="w-full" selectname="kota" selectid="kota" />
        </div>
      </div>

      <!-- Submit Button -->
      <div class="flex justify-end mt-5">
        <button class="py-2 px-6 bg-[#009efb] rounded-lg text-white hover:scale-95 duration-150 transition-all">Terapkan</button>
      </div>
    </form>
  </div>

  <div class="mt-5 w-full">
    <div class="w-full bg-white py-5 px-12 rounded-3xl text-black">
      <EntriesValue />

      <div class="w-full mt-5">
        <table class="w-full table-auto border-collapse">
          <thead>
            <tr class="border-b-1 border-gray-200 text-left">
              <th class="py-3">No</th>
              <th class="py-3">Jenis Daerah</th>
              <th class="py-3">Jumlah</th>
              <th class="py-3">%</th>
              <th class="py-3">Keterangan</th>
            </tr>
          </thead>
          <tbody>
            <tr class="border-b border-gray-200">
              <td class="py-3">1</td>
              <td class="py-3">Prov</td>
              <td class="py-3">0</td>
              <td class="py-3">0</td>
              <td class="py-3">Lorem ipsum dolor sit amet</td>
            </tr>
            <tr class="border-b border-gray-200">
              <td class="py-3">2</td>
              <td class="py-3">Kab/kota</td>
              <td class="py-3">0</td>
              <td class="py-3">0</td>
              <td class="py-3">Lorem ipsum dolor sit amet</td>
            </tr>
            <!-- Total row -->
            <tr class="font-bold border-t-1 border-gray-300">
              <td class="py-3"></td>
              <td class="py-3">Total</td>
              <td class="py-3">0</td>
              <td class="py-3">0</td>
              <td class="py-3"></td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>

  <TabsSystem2 />
</template>
