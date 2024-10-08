<template>
  <div class="flex justify-between items-center">
    <div class="">
      <h1 class="text-2xl text-black">
        {{ typeof $route.params.province === "string" ? $route.params.province.toUpperCase() : "" }}
      </h1>

      <Breadcrumb :province="$route.params.province" />
    </div>
    <div class="">
      <SelectYear />
    </div>
  </div>

  <div class="w-full bg-white mt-6 rounded-3xl">
    <div class="w-full h-16 bg-[#ff9000] rounded-tr-2xl rounded-tl-2xl rounded- text-white p-5 text-xl">
      <h1>Informasi Daerah</h1>
    </div>
    <div class="flex flex-row p-10 items-center">
      <img class="w-60 h-60 mr-10" src="@/assets/images/aceh.png" alt="logo" />
      <div class="flex flex-col w-full">
        <div class="border-b-2 pb-5">
          <h1 class="text-2xl font-medium">
            {{ typeof $route.params.province === "string" ? $route.params.province.toUpperCase() : "" }}
          </h1>
          <h1>PERIODE RPJMD (2018 - 2023) - "Terwujudnya Aceh Selatan yang Bekeadilan Secara Sosial dan Ekonomi"</h1>
        </div>
        <div class="flex flex-col gap-2 pt-5">
          <div class="flex flex-row border-2">
            <div class="p-3">Nama Kepala Daerah</div>
            <div class="border-x p-3">:</div>
            <div class="flex flex-1 p-3"></div>
          </div>
          <h1 class="text-lg font-semibold">Tahapan</h1>
          <h1>-</h1>
        </div>
      </div>
    </div>
  </div>
  
  <TablePagu />
</template>
