<script setup>
// onMounted
import { ref, computed } from "vue";
import { Chart } from "chart.js/auto";
import StatusCard from "../components/StatusCard.vue";
import LabelColor from "./dashboard/LandingReadme/LabelColor.vue";

const searchTerm = ref("");

const filteredData = computed(() => {
  if (!searchTerm.value) return selectedData.value;
  return selectedData.value.filter(
    (item) =>
      item.namapemda.toLowerCase().includes(searchTerm.value.toLowerCase()) || item.kodepemda.includes(searchTerm.value) || item.nama_sub_tahap.toLowerCase().includes(searchTerm.value.toLowerCase())
  );
});

const data = ref({
  singkat: {
    tahun: "2022",
    beluminput: 4,
    rancangan: 0,
    ranwal: 0,
    musrenbang: 0,
    rancanganakhir: 0,
    totalprov: 38,
    penetapan: 1,
    rancangan_kua_ppas: 0,
    penetapan_kua_ppas: 1,
    rancangan_apbd: 10,
    penetapan_apbd: 0,
  },
  detail: {
    beluminput: [
      {
        tahun: "2022",
        provno: "93",
        kabkotno: "00",
        kodepemda: "9300",
        namapemda: "PAPUA SELATAN",
        waktu_mulai: "",
        waktu_selesai: "",
        nama_sub_tahap: "-",
        berlangsung: 0,
      },
      {
        tahun: "2022",
        provno: "94",
        kabkotno: "00",
        kodepemda: "9400",
        namapemda: "PAPUA TENGAH",
        waktu_mulai: "",
        waktu_selesai: "",
        nama_sub_tahap: "-",
        berlangsung: 0,
      },
      {
        tahun: "2022",
        provno: "95",
        kabkotno: "00",
        kodepemda: "9500",
        namapemda: "PAPUA PEGUNUNGAN",
        waktu_mulai: "",
        waktu_selesai: "",
        nama_sub_tahap: "-",
        berlangsung: 0,
      },
      {
        tahun: "2022",
        provno: "96",
        kabkotno: "00",
        kodepemda: "9600",
        namapemda: "PAPUA BARAT DAYA",
        waktu_mulai: "",
        waktu_selesai: "",
        nama_sub_tahap: "-",
        berlangsung: 0,
      },
    ],
    rancangan: [],
    ranwal: [],
    musrenbang: [],
    rancanganakhir: [],
    penetapan: [
      {
        tahun: "2022",
        provno: "33",
        kabkotno: "00",
        kodepemda: "3300",
        namapemda: "JAWA TENGAH",
        waktu_mulai: "15\/10\/2021 09:00",
        waktu_selesai: "31\/10\/2021 00:00",
        nama_sub_tahap: "Penetapan",
        berlangsung: 0,
      },
    ],
    rancangan_kua_ppas: [],
    penetapan_kua_ppas: [
      {
        tahun: "2022",
        provno: "31",
        kabkotno: "00",
        kodepemda: "3100",
        namapemda: "DKI JAKARTA",
        waktu_mulai: "23\/11\/2021 00:00",
        waktu_selesai: "21\/02\/2022 10:00",
        nama_sub_tahap: "KUA dan PPAS ",
        berlangsung: 0,
      },
    ],
    rancangan_apbd: [
      {
        tahun: "2022",
        provno: "16",
        kabkotno: "00",
        kodepemda: "1600",
        namapemda: "SUMATERA SELATAN",
        waktu_mulai: "15\/11\/2021 10:29",
        waktu_selesai: "23\/11\/2021 10:01",
        nama_sub_tahap: "RAPBD Bahan Rapat Komisi DPRD",
        berlangsung: 0,
      },
      {
        tahun: "2022",
        provno: "19",
        kabkotno: "00",
        kodepemda: "1900",
        namapemda: "KEPULAUAN BANGKA BELITUNG",
        waktu_mulai: "31\/12\/2021 20:10",
        waktu_selesai: "10\/01\/2022 13:55",
        nama_sub_tahap: "RAPBD TAHAP PENYESUAIAN HASIL EVALUASI",
        berlangsung: 0,
      },
      {
        tahun: "2022",
        provno: "21",
        kabkotno: "00",
        kodepemda: "2100",
        namapemda: "KEPULAUAN RIAU",
        waktu_mulai: "14\/11\/2021 19:00",
        waktu_selesai: "23\/12\/2021 06:20",
        nama_sub_tahap: "RANCANGAN ANGGARAN PENDAPATAN BELANJA DAERAH TA 2022",
        berlangsung: 0,
      },
      {
        tahun: "2022",
        provno: "32",
        kabkotno: "00",
        kodepemda: "3200",
        namapemda: "JAWA BARAT",
        waktu_mulai: "30\/11\/2021 21:50",
        waktu_selesai: "30\/11\/2021 21:53",
        nama_sub_tahap: "Raperda Nota Keuangan",
        berlangsung: 0,
      },
      {
        tahun: "2022",
        provno: "36",
        kabkotno: "00",
        kodepemda: "3600",
        namapemda: "BANTEN",
        waktu_mulai: "28\/09\/2021 18:00",
        waktu_selesai: "04\/10\/2021 18:00",
        nama_sub_tahap: "Penyusunan Rancangan APBD",
        berlangsung: 0,
      },
      {
        tahun: "2022",
        provno: "65",
        kabkotno: "00",
        kodepemda: "6500",
        namapemda: "KALIMANTAN UTARA",
        waktu_mulai: "02\/12\/2021 15:00",
        waktu_selesai: "02\/12\/2021 15:57",
        nama_sub_tahap: "Penyusunan R APBD",
        berlangsung: 0,
      },
      {
        tahun: "2022",
        provno: "72",
        kabkotno: "00",
        kodepemda: "7200",
        namapemda: "SULAWESI TENGAH",
        waktu_mulai: "09\/11\/2021 00:00",
        waktu_selesai: "17\/11\/2021 12:51",
        nama_sub_tahap: "RAPBD - AWAL",
        berlangsung: 0,
      },
      {
        tahun: "2022",
        provno: "74",
        kabkotno: "00",
        kodepemda: "7400",
        namapemda: "SULAWESI TENGGARA",
        waktu_mulai: "29\/11\/2021 09:12",
        waktu_selesai: "29\/11\/2021 09:20",
        nama_sub_tahap: "Penyusunan dan Pembahasan RAPBD ",
        berlangsung: 0,
      },
      {
        tahun: "2022",
        provno: "76",
        kabkotno: "00",
        kodepemda: "7600",
        namapemda: "SULAWESI BARAT",
        waktu_mulai: "26\/11\/2021 08:00",
        waktu_selesai: "02\/12\/2021 11:34",
        nama_sub_tahap: "Rancangan APBD 2022",
        berlangsung: 0,
      },
      {
        tahun: "2022",
        provno: "91",
        kabkotno: "00",
        kodepemda: "9100",
        namapemda: "P A P U A",
        waktu_mulai: "16\/12\/2021 00:00",
        waktu_selesai: "22\/12\/2021 20:22",
        nama_sub_tahap: "RANCANGAN APBD TA 2022 ",
        berlangsung: 0,
      },
    ],
    penetapan_apbd: [],
  },
  chart: {
    label: ["Belum Input", "Ranwal", "Rancangan", "Musrenbang", "Rancangan Akhir", "Penetapan", "Rancangan KUA dan PPAS", "Penetapan KUA dan PPAS", "Rancangan APBD", "Penetapan APBD"],
    value: [4, 7, 9, 12, 5, 3, 5, 10, 10, 9],
  },
});

const rkpdCards = {
  beluminput: { color: "#ff2f55", label: "Belum Input" },
  rancangan: { color: "#39c449", label: "Rancangan awal" },
  ranwal: { color: "#263238", label: "Rancangan" },
  musrenbang: { color: "#ffbc34", label: "Musrenbang" },
  rancanganakhir: { color: "#7460ee", label: "Rancangan Akhir" },
  penetapan: { color: "#009efb", label: "Penetapan" },
};

const kuaPpasCards = {
  rancangan_kua_ppas: { color: "#cd69c9", label: "Rancangan " },
  penetapan_kua_ppas: { color: "#cd3178", label: "Penetapan " },
};

const apbdCards = {
  rancangan_apbd: { color: "#b3ee3a", label: "Rancangan " },
  penetapan_apbd: { color: "#cebe70", label: "Penetapan " },
};

const showModal = ref(false);
const selectedCard = ref("");
const selectedData = ref([]);
const toggleBodyScroll = (disable) => {
  if (disable) {
    document.body.classList.add("modal-open");
  } else {
    document.body.classList.remove("modal-open");
  }
};
const openModal = (key) => {
  const allCards = { ...rkpdCards, ...kuaPpasCards, ...apbdCards };
  selectedCard.value = allCards[key].label;
  selectedData.value = data.value.detail[key];
  showModal.value = true;
  setTimeout(() => toggleBodyScroll(true), 300);
};

const closeModal = () => {
  showModal.value = false;
  setTimeout(() => toggleBodyScroll(false), 200);
};

onMounted(() => {
  const ctx = document.getElementById("myChart");
  if (ctx) {
    const chartData = {
      labels: data.value.chart.label,
      datasets: [
        {
          label: "Chart Rekap Tahapan Per-Provinsi " + data.value.singkat.tahun,
          data: data.value.chart.value,
          backgroundColor: ["#ff2f55", "#39c449", "#263238", "#ffbc34", "#7460ee", "#009efb", "#cd69c9", "#cd3178", "#b3ee3a", "#cebe70"],
          hoverOffset: 10,
          borderWidth: 0,
        },
      ],
    };

    const chartInstance = new Chart(ctx, {
      type: "doughnut",
      data: chartData,
      options: {
        responsive: true,
        maintainAspectRatio: true,
        plugins: {
          legend: {
            position: "center",
            align: "start",
            maxHeight: "500",
            width: "500",
          },
        },
        layout: {
          padding: {
            top: 10,
            bottom: 10,
          },
        },
      },
    });
  }
});
</script>

<template>
  <div class="flex flex-col gap-4">
    <div class="flex justify-between items-center self-center w-full">
      <div class="">
        <h1 class="text-2xl text-black">Dashboard</h1>
      </div>
      <div class="h-auto w-auto">
        <div class="">
          <SelectYear />
        </div>
      </div>
    </div>
    <div class="text-lg w-full py-3 px-5 bg-[#ccecfe] text-[#5E5E5E] border border-[#b8e4fe] rounded-md">
      <div class="">
        Posisi Per-Provinsi Tahun:
        <b class="text-black">{{ data.singkat.tahun }}</b>
      </div>
    </div>
  </div>

  <div class="flex flex-col gap-5 py-5">
    <div class="flex flex-col lg:flex-row gap-5">
      <div class="bg-white px-4 sm:px-9 py-3 sm:py-5 lg:p-8 rounded-3xl flex flex-col gap-3 text-white w-full">
        <h1 class="text-xl text-black font-medium mb-2">RKPD</h1>
        <div class="w-full grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-5 sm:gap-5 lg:gap-3 mb-8">
          <StatusCard v-for="(card, key) in rkpdCards" :key="key" :color="card.color" :value="data.singkat[key]" :label="card.label" @card-click="openModal(key)" />
        </div>
      </div>

      <div class="flex flex-col sm:flex-row gap-5 w-full">
        <div class="bg-white px-4 sm:px-9 py-3 sm:py-5 lg:p-8 rounded-3xl flex flex-col gap-3 text-white w-full">
          <h1 class="text-xl text-black font-medium mb-2">KUA dan PPAS</h1>
          <div class="w-full grid grid-cols-1 sm:grid-cols-1 gap-5 sm:gap-5 lg:gap-3 mb-8">
            <StatusCard v-for="(card, key) in kuaPpasCards" :key="key" :color="card.color" :value="data.singkat[key]" :label="card.label" @card-click="openModal(key)" />
          </div>
        </div>

        <div class="bg-white px-4 sm:px-9 py-3 sm:py-5 lg:p-8 rounded-3xl flex flex-col gap-3 text-white w-full">
          <h1 class="text-xl text-black font-medium mb-2">APBD</h1>
          <div class="w-full grid grid-cols-1 sm:grid-cols-1 gap-5 sm:gap-5 lg:gap-3 mb-8">
            <StatusCard v-for="(card, key) in apbdCards" :key="key" :color="card.color" :value="data.singkat[key]" :label="card.label" @card-click="openModal(key)" />
          </div>
        </div>
      </div>
    </div>

    <div class="justify-center bg-white rounded-3xl sm:px-5 p-10 grid lg:flex items-center h-full gap-10 lg:max-h-[600px]">
      <canvas id="myChart"></canvas>
      <LabelColor />
    </div>
  </div>

  <!-- Modal -->
  <div v-show="showModal" class="fixed top-0 inset-0 bg-black bg-opacity-70 flex items-center justify-center z-[500] py-[10px] overflow-auto">
    <transition name="modal-drop">
      <div v-show="showModal" class="bg-white rounded sm:w-full md:w-3/4 overflow-auto">
        <h2 class="text-lg bg-[#009efb] p-4 text-white">Detail: {{ selectedCard }}</h2>
        <div class="p-4">
          <div class="mb-4">
            <input v-model="searchTerm" type="text" placeholder="Search..." class="w-full p-2 border border-gray-300 outline-none rounded" />
          </div>
          <div class="overflow-auto">
            <div class="">
              <table class="w-full border-collapse border border-gray-300">
                <thead>
                  <tr>
                    <th class="border border-gray-300 p-2">No</th>
                    <th class="border border-gray-300 p-2">Provinsi</th>
                    <th class="border border-gray-300 p-2">Kodepemda</th>
                    <th class="border border-gray-300 p-2">Tahapan Akhir di SIPD</th>
                  </tr>
                </thead>
                <tbody>
                  <tr v-for="(item, index) in filteredData" :key="index">
                    <td class="border border-gray-300 p-2">{{ index + 1 }}</td>
                    <td class="border border-gray-300 p-2">
                      {{ item.namapemda }}
                    </td>
                    <td class="border border-gray-300 p-2">
                      {{ item.kodepemda }}
                    </td>
                    <td class="border border-gray-300 p-2">
                      <h1>{{ item.nama_sub_tahap }}</h1>
                      <h1 class="w-fit bg-[#f62d51] text-white text-sm p-1 rounded">
                        Tanggal: {{ item.waktu_mulai }} s/d
                        {{ item.waktu_selesai }}
                      </h1>
                    </td>
                  </tr>
                </tbody>
              </table>
            </div>
          </div>
        </div>

        <div class="p-4 flex justify-end content-center border-t-2">
          <button @click="closeModal" class="bg-[#868e96] text-white px-4 py-2 rounded">Tutup</button>
        </div>
      </div>
    </transition>
  </div>
</template>

<style scoped>
.modal-drop-enter-active,
.modal-drop-leave-active {
  transition: all 0.3s ease;
}

.modal-drop-enter-from,
.modal-drop-leave-to {
  transform: translateY(-50px);
  opacity: 0;
}
</style>
