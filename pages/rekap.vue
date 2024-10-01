<script setup>
const { data: tahapan } = await useAsyncData("tahapan", () => $fetch("https://cdn.kotakpasir.dev/edb-gis/2024%2Frekap_perprovinsi.json"));

const { data: Rekapdata_tahapan } = await useAsyncData("Rekapdata_tahapan", () => $fetch("https://cdn.kotakpasir.dev/edb-gis/2024%2Frekap_tahapan_data_rkpd.json"));

const { data: detailTahapan } = await useAsyncData("detailTahapan", () => $fetch("https://cdn.kotakpasir.dev/edb-gis/2024%2Fjumlah_rekap%20_tahapan_dikab_kota_perprovinsi.json"));

const { data: testrekapperbidang_prov } = await useAsyncData("testrekapperbidang_prov", () => $fetch("https://cdn.kotakpasir.dev/edb-gis/2024%2Frekap_anggaran_perbidang_urusan_provinsi.json"));
</script>

<template>
  <div>
    <RekapTitle />

    <div class="overflow-auto mt-5 rounded">
      <h2 class="text-base bg-[#009efb] p-5 text-white">Tahapan Perprovinsi {{ tahapan.tahun }}</h2>
      <div class="p-5 bg-white w-full">
        <RekapTableTahapanPerprovinsi :data="tahapan.data" />
      </div>
    </div>

    <div class="overflow-auto mt-5 rounded">
      <h2 class="text-base bg-[#ffbc34] p-5">REKAP DATA TAHAPAN RKPD {{ Rekapdata_tahapan.tahun }} SIPD</h2>
      <div class="bg-white rounded w-full">
        <RekapTableTahapanRKPD :data="Rekapdata_tahapan.data" />
      </div>
    </div>

    <div class="overflow-auto mt-5 rounded">
      <h2 class="text-base bg-[#ffbc34] p-5">Jumlah Rekap Tahapan di Kab/Kota Per-Provinsi</h2>
      <div class="bg-white rounded w-full">
        <RekapTableTahapanKabupaten :data="detailTahapan.data" />
      </div>
    </div>

    <div class="overflow-auto mt-5 rounded">
      <h2 class="text-base bg-[#ffbc34] p-5">Rekap Per Bidang Urusan Pemda</h2>
      <div class="bg-white rounded w-full">
        <RekapTablePerBidangUrusanPemda :data="testrekapperbidang_prov.data" />
      </div>
    </div>
  </div>
</template>
