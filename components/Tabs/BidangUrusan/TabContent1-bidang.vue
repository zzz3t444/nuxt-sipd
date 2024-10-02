<template>
  <div class="mt-5 w-full bg-white py-12 px-7 rounded-3xl text-white">
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
