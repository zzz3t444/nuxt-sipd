<script setup>
import Province from "../utils/provinceListName.json";
import sumberDanaData from "../utils/SumberDana.json";

const sumberDana = sumberDanaData;
import subKegiatanData from "../utils/SubKegiatan.json";
const subKegiatan = subKegiatanData;
</script>

<template>
  <main>
    <div class="flex justify-between items-center">
      <div class="">
        <h1 class="text-2xl text-black">Sumber Pendanaan</h1>
        <h1 class="text-sm text-neutral-500">
          <NuxtLink to="/" class="text-[#009efb] hover:text-[#7460e]">Dashboard</NuxtLink>
          >
          <NuxtLink to="/" class="text-[#009efb] hover:text-[#7460e]">Informasi Pembangunan Daerah</NuxtLink>
          > Sumber Pendanaan
        </h1>
      </div>
      <div class="">
        <SelectYear />
      </div>
    </div>

    <div class="bg-white w-full px-4 sm:px-20 py-10 rounded-3xl my-8">
      <form class="flex flex-col gap-3 w-full">
        <div class="flex flex-col md:flex-row items-center gap-5">
          <div class="flex flex-col gap-2 w-full md:w-[50%]">
            <label for="Provinsi" class="text-black">Provinsi</label>
            <SelectInput :render="Province" class="w-full" selectname="Provinsi" selectid="Provinsi" />
          </div>
          <div class="flex flex-col gap-2 w-full md:w-[50%]">
            <label for="Kab/Kota" class="text-black">Kab/Kota</label>
            <MultipleSelectInput :render="sumberDanaData" class="w-full" selectname="subkegiatan" selectid="subkegiatan" />
          </div>
        </div>

        <div class="items-center gap-5">
          <div class="w-full">
            <label for="Sumberdana" class="text-black">Pilih Sumberdana</label>
            <MultipleSelectInput :render="sumberDana" class="w-full mt-2" selectname="sumberDana" selectid="sumberDana" />
          </div>
        </div>

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
                <th class="py-3">Kode Pemda</th>
                <th class="py-3">Nama Pemda</th>
                <th class="py-3 text-center" colspan="2">Sumberdana</th>
              </tr>
              <tr class="border-b-1 border-gray-200 text-left">
                <th class="py-3"></th>
                <th class="py-3"></th>
                <th class="py-3"></th>
                <th class="py-3">Kode</th>
                <th class="py-3">Urai</th>
                <th class="py-3">Pagu</th>
                <th class="py-3"></th>
              </tr>
            </thead>
            <tbody>
              <tr class="border-b border-gray-200">
                <td class="py-3">1</td>
                <td class="py-3">-</td>
                <td class="py-3">-</td>
                <td class="py-3">-</td>
                <td class="py-3">-</td>
                <td class="py-3">-</td>
              </tr>
            </tbody>
          </table>
          <div class="mt-3 text-right">
            <p>Data Update: -</p>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>
