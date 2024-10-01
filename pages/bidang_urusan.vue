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
  <div class="bg-white w-full px-4 sm:px-14 py-4 rounded-lg my-8">
    <form class="flex flex-col gap-3 w-full">
      <div class="flex items-center gap-5">
        <div class="flex flex-col gap-2 w-[50%]">
          <label for="tema" class="text-black">Pilih Tema</label>
          <SelectInput :render="temaList" class="w-full" selectname="tema" selectid="tema" />
        </div>
        <div class="flex flex-col gap-2 w-[50%]">
          <label for="tema" class="text-black">Pilih Sub kegiatan</label>
          <MultipleSelectInput :render="subKegiatan" class="w-full" selectname="subkegiatan" selectid="subkegiatan" />
        </div>
      </div>
      <div class="flex flex-col gap-2 w-[100%]">
        <label for="tema" class="text-black">Lingkup</label>
        <SelectInput :render="lingkup" class="w-full" selectname="lingkup" selectid="lingkup" />
      </div>
      <div class="flex items-center gap-5">
        <div class="flex flex-col gap-2 w-[50%]">
          <label for="tema" class="text-black">Provinsi</label>
          <SelectInput :render="temaList" class="w-full" selectname="lingkup" selectid="lingkup" />
        </div>
        <div class="flex flex-col gap-2 w-[50%]">
          <label for="tema" class="text-black">Kab / Kota</label>
          <SelectInput :render="temaList" class="w-full" selectname="lingkup" selectid="lingkup" />
        </div>
      </div>
      <div class="flex justify-end mt-5 mb-5">
        <button class="py-2 px-6 bg-[#009efb] rounded-lg text-white hover:scale-95 duration-150 transition-all">Terapkan</button>
      </div>
    </form>
  </div>
  <div class="mt-16 w-full">
    <div class="flex justify-between items-center flex-wrap">
      <SearchInput searchname="search" searchid="search" />
      <Menu />
    </div>
    <div class="mt-5 w-full bg-[#272B34] py-10 px-7 rounded-lg text-white">
      <header class="flex items-center gap-4">
        <span>Show</span>
        <select name="entriescount" id="entriescount" class="py-2 px-3 w-[100px] outline-none rounded-md text-left bg-[#323743]">
          <option value="10">10</option>
          <option value="50">50</option>
          <option value="100" selected>100</option>
        </select>
        <span>Entries</span>
      </header>
      <div class="w-full mt-5">
        <table class="w-full">
          <thead>
            <th>No</th>
            <th>Jenis Daerah</th>
            <th>Jumlah</th>
            <th>%{?}</th>
            <th>Keterangan</th>
          </thead>
          <tbody>
            <tr class="border-t-2">
              <td class="py-8">1</td>
              <td class="py-8">Prov</td>
              <td class="py-8">0</td>
              <td class="py-8">0</td>
              <td class="py-8">Lorem ipsum dolor sit amet</td>
            </tr>
            <tr class="border-t-2">
              <td class="py-8">2</td>
              <td class="py-8">Kab/kota</td>
              <td class="py-8">0</td>
              <td class="py-8">0</td>
              <td class="py-8">Lorem ipsum dolor sit amet</td>
            </tr>
          </tbody>
        </table>
      </div>
      <footer class="flex justify-between items-center">
        <span class="font-bold"> Total: </span>
        <span class="font-bold">0.00</span>
        <div class="flex w-[200px] border-2 border-sky-500 rounded-xl">
          <a href="#" class="w-1/3 p-2 bg-sky-500 text-center rounded-l-lg">PREV</a>
          <span class="w-1/3 p-2 text-center">1</span>
          <a href="#" class="w-1/3 p-2 bg-sky-500 text-center rounded-r-lg">NEXT</a>
        </div>
      </footer>
    </div>
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
