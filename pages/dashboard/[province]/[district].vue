<script setup>
import { onMounted, ref, computed } from "vue";
import { Chart } from "chart.js/auto";
import StatusCard from "../components/StatusCard.vue";

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
    tahun: "2025",
    beluminput: 23,
    persiapan: 0,
    rancangan: 0,
    ranwal: 0,
    musrenbang: 0,
    rancanganakhir: 0,
    totalprov: 23,
    penetapan: 0,
  },
  detail: {
    beluminput: [
      {
        tahun: "2025",
        provno: "11",
        kabkotno: "01",
        kodepemda: "1101",
        namapemda: "KAB. ACEH SELATAN",
        waktu_mulai: "",
        waktu_selesai: "",
        nama_sub_tahap: "-",
        berlangsung: 0,
      },
      {
        tahun: "2025",
        provno: "11",
        kabkotno: "02",
        kodepemda: "1102",
        namapemda: "KAB. ACEH TENGGARA",
        waktu_mulai: "",
        waktu_selesai: "",
        nama_sub_tahap: "-",
        berlangsung: 0,
      },
      {
        tahun: "2025",
        provno: "11",
        kabkotno: "03",
        kodepemda: "1103",
        namapemda: "KAB. ACEH TIMUR",
        waktu_mulai: "",
        waktu_selesai: "",
        nama_sub_tahap: "-",
        berlangsung: 0,
      },
      {
        tahun: "2025",
        provno: "11",
        kabkotno: "04",
        kodepemda: "1104",
        namapemda: "KAB. ACEH TENGAH",
        waktu_mulai: "",
        waktu_selesai: "",
        nama_sub_tahap: "-",
        berlangsung: 0,
      },
      {
        tahun: "2025",
        provno: "11",
        kabkotno: "05",
        kodepemda: "1105",
        namapemda: "KAB. ACEH BARAT",
        waktu_mulai: "",
        waktu_selesai: "",
        nama_sub_tahap: "-",
        berlangsung: 0,
      },
      {
        tahun: "2025",
        provno: "11",
        kabkotno: "06",
        kodepemda: "1106",
        namapemda: "KAB. ACEH BESAR",
        waktu_mulai: "",
        waktu_selesai: "",
        nama_sub_tahap: "-",
        berlangsung: 0,
      },
      {
        tahun: "2025",
        provno: "11",
        kabkotno: "07",
        kodepemda: "1107",
        namapemda: "KAB. PIDIE",
        waktu_mulai: "",
        waktu_selesai: "",
        nama_sub_tahap: "-",
        berlangsung: 0,
      },
      {
        tahun: "2025",
        provno: "11",
        kabkotno: "08",
        kodepemda: "1108",
        namapemda: "KAB. ACEH UTARA",
        waktu_mulai: "",
        waktu_selesai: "",
        nama_sub_tahap: "-",
        berlangsung: 0,
      },
      {
        tahun: "2025",
        provno: "11",
        kabkotno: "09",
        kodepemda: "1109",
        namapemda: "KAB. SIMEULUE",
        waktu_mulai: "",
        waktu_selesai: "",
        nama_sub_tahap: "-",
        berlangsung: 0,
      },
      {
        tahun: "2025",
        provno: "11",
        kabkotno: "10",
        kodepemda: "1110",
        namapemda: "KAB. ACEH SINGKIL",
        waktu_mulai: "",
        waktu_selesai: "",
        nama_sub_tahap: "-",
        berlangsung: 0,
      },
      {
        tahun: "2025",
        provno: "11",
        kabkotno: "11",
        kodepemda: "1111",
        namapemda: "KAB. BIREUEN",
        waktu_mulai: "",
        waktu_selesai: "",
        nama_sub_tahap: "-",
        berlangsung: 0,
      },
      {
        tahun: "2025",
        provno: "11",
        kabkotno: "12",
        kodepemda: "1112",
        namapemda: "KAB. ACEH BARAT DAYA",
        waktu_mulai: "",
        waktu_selesai: "",
        nama_sub_tahap: "-",
        berlangsung: 0,
      },
      {
        tahun: "2025",
        provno: "11",
        kabkotno: "13",
        kodepemda: "1113",
        namapemda: "KAB. GAYO LUES",
        waktu_mulai: "",
        waktu_selesai: "",
        nama_sub_tahap: "-",
        berlangsung: 0,
      },
      {
        tahun: "2025",
        provno: "11",
        kabkotno: "14",
        kodepemda: "1114",
        namapemda: "KAB. ACEH JAYA",
        waktu_mulai: "",
        waktu_selesai: "",
        nama_sub_tahap: "-",
        berlangsung: 0,
      },
      {
        tahun: "2025",
        provno: "11",
        kabkotno: "15",
        kodepemda: "1115",
        namapemda: "KAB. NAGAN RAYA",
        waktu_mulai: "",
        waktu_selesai: "",
        nama_sub_tahap: "-",
        berlangsung: 0,
      },
      {
        tahun: "2025",
        provno: "11",
        kabkotno: "16",
        kodepemda: "1116",
        namapemda: "KAB. ACEH TAMIANG",
        waktu_mulai: "",
        waktu_selesai: "",
        nama_sub_tahap: "-",
        berlangsung: 0,
      },
      {
        tahun: "2025",
        provno: "11",
        kabkotno: "17",
        kodepemda: "1117",
        namapemda: "KAB. BENER MERIAH",
        waktu_mulai: "",
        waktu_selesai: "",
        nama_sub_tahap: "-",
        berlangsung: 0,
      },
      {
        tahun: "2025",
        provno: "11",
        kabkotno: "18",
        kodepemda: "1118",
        namapemda: "KAB. PIDIE JAYA",
        waktu_mulai: "",
        waktu_selesai: "",
        nama_sub_tahap: "-",
        berlangsung: 0,
      },
      {
        tahun: "2025",
        provno: "11",
        kabkotno: "71",
        kodepemda: "1171",
        namapemda: "KOTA BANDA ACEH",
        waktu_mulai: "",
        waktu_selesai: "",
        nama_sub_tahap: "-",
        berlangsung: 0,
      },
      {
        tahun: "2025",
        provno: "11",
        kabkotno: "72",
        kodepemda: "1172",
        namapemda: "KOTA SABANG",
        waktu_mulai: "",
        waktu_selesai: "",
        nama_sub_tahap: "-",
        berlangsung: 0,
      },
      {
        tahun: "2025",
        provno: "11",
        kabkotno: "73",
        kodepemda: "1173",
        namapemda: "KOTA LHOKSEUMAWE",
        waktu_mulai: "",
        waktu_selesai: "",
        nama_sub_tahap: "-",
        berlangsung: 0,
      },
      {
        tahun: "2025",
        provno: "11",
        kabkotno: "74",
        kodepemda: "1174",
        namapemda: "KOTA LANGSA",
        waktu_mulai: "",
        waktu_selesai: "",
        nama_sub_tahap: "-",
        berlangsung: 0,
      },
      {
        tahun: "2025",
        provno: "11",
        kabkotno: "75",
        kodepemda: "1175",
        namapemda: "KOTA SUBULUSSALAM",
        waktu_mulai: "",
        waktu_selesai: "",
        nama_sub_tahap: "-",
        berlangsung: 0,
      },
    ],
    persiapan: [],
    rancangan: [],
    ranwal: [],
    musrenbang: [],
    rancanganakhir: [],
    penetapan: [],
  },
  chart: {
    label: ["Belum Input", "Persiapan", "Ranwal", "Rancangan", "Musrenbang", "Rancangan Akhir", "Penetapan"],
    value: [23, 0, 0, 0, 0, 0, 0],
  },
  data: [
    {
      tahun: "2025",
      provno: "11",
      kabkotno: "01",
      kodepemda: "1101",
      namapemda: "KAB. ACEH SELATAN",
      waktu_mulai: "",
      waktu_selesai: "",
      nama_sub_tahap: "-",
      berlangsung: 0,
    },
    {
      tahun: "2025",
      provno: "11",
      kabkotno: "02",
      kodepemda: "1102",
      namapemda: "KAB. ACEH TENGGARA",
      waktu_mulai: "",
      waktu_selesai: "",
      nama_sub_tahap: "-",
      berlangsung: 0,
    },
    {
      tahun: "2025",
      provno: "11",
      kabkotno: "03",
      kodepemda: "1103",
      namapemda: "KAB. ACEH TIMUR",
      waktu_mulai: "",
      waktu_selesai: "",
      nama_sub_tahap: "-",
      berlangsung: 0,
    },
    {
      tahun: "2025",
      provno: "11",
      kabkotno: "04",
      kodepemda: "1104",
      namapemda: "KAB. ACEH TENGAH",
      waktu_mulai: "",
      waktu_selesai: "",
      nama_sub_tahap: "-",
      berlangsung: 0,
    },
    {
      tahun: "2025",
      provno: "11",
      kabkotno: "05",
      kodepemda: "1105",
      namapemda: "KAB. ACEH BARAT",
      waktu_mulai: "",
      waktu_selesai: "",
      nama_sub_tahap: "-",
      berlangsung: 0,
    },
    {
      tahun: "2025",
      provno: "11",
      kabkotno: "06",
      kodepemda: "1106",
      namapemda: "KAB. ACEH BESAR",
      waktu_mulai: "",
      waktu_selesai: "",
      nama_sub_tahap: "-",
      berlangsung: 0,
    },
    {
      tahun: "2025",
      provno: "11",
      kabkotno: "07",
      kodepemda: "1107",
      namapemda: "KAB. PIDIE",
      waktu_mulai: "",
      waktu_selesai: "",
      nama_sub_tahap: "-",
      berlangsung: 0,
    },
    {
      tahun: "2025",
      provno: "11",
      kabkotno: "08",
      kodepemda: "1108",
      namapemda: "KAB. ACEH UTARA",
      waktu_mulai: "",
      waktu_selesai: "",
      nama_sub_tahap: "-",
      berlangsung: 0,
    },
    {
      tahun: "2025",
      provno: "11",
      kabkotno: "09",
      kodepemda: "1109",
      namapemda: "KAB. SIMEULUE",
      waktu_mulai: "",
      waktu_selesai: "",
      nama_sub_tahap: "-",
      berlangsung: 0,
    },
    {
      tahun: "2025",
      provno: "11",
      kabkotno: "10",
      kodepemda: "1110",
      namapemda: "KAB. ACEH SINGKIL",
      waktu_mulai: "",
      waktu_selesai: "",
      nama_sub_tahap: "-",
      berlangsung: 0,
    },
    {
      tahun: "2025",
      provno: "11",
      kabkotno: "11",
      kodepemda: "1111",
      namapemda: "KAB. BIREUEN",
      waktu_mulai: "",
      waktu_selesai: "",
      nama_sub_tahap: "-",
      berlangsung: 0,
    },
    {
      tahun: "2025",
      provno: "11",
      kabkotno: "12",
      kodepemda: "1112",
      namapemda: "KAB. ACEH BARAT DAYA",
      waktu_mulai: "",
      waktu_selesai: "",
      nama_sub_tahap: "-",
      berlangsung: 0,
    },
    {
      tahun: "2025",
      provno: "11",
      kabkotno: "13",
      kodepemda: "1113",
      namapemda: "KAB. GAYO LUES",
      waktu_mulai: "",
      waktu_selesai: "",
      nama_sub_tahap: "-",
      berlangsung: 0,
    },
    {
      tahun: "2025",
      provno: "11",
      kabkotno: "14",
      kodepemda: "1114",
      namapemda: "KAB. ACEH JAYA",
      waktu_mulai: "",
      waktu_selesai: "",
      nama_sub_tahap: "-",
      berlangsung: 0,
    },
    {
      tahun: "2025",
      provno: "11",
      kabkotno: "15",
      kodepemda: "1115",
      namapemda: "KAB. NAGAN RAYA",
      waktu_mulai: "",
      waktu_selesai: "",
      nama_sub_tahap: "-",
      berlangsung: 0,
    },
    {
      tahun: "2025",
      provno: "11",
      kabkotno: "16",
      kodepemda: "1116",
      namapemda: "KAB. ACEH TAMIANG",
      waktu_mulai: "",
      waktu_selesai: "",
      nama_sub_tahap: "-",
      berlangsung: 0,
    },
    {
      tahun: "2025",
      provno: "11",
      kabkotno: "17",
      kodepemda: "1117",
      namapemda: "KAB. BENER MERIAH",
      waktu_mulai: "",
      waktu_selesai: "",
      nama_sub_tahap: "-",
      berlangsung: 0,
    },
    {
      tahun: "2025",
      provno: "11",
      kabkotno: "18",
      kodepemda: "1118",
      namapemda: "KAB. PIDIE JAYA",
      waktu_mulai: "",
      waktu_selesai: "",
      nama_sub_tahap: "-",
      berlangsung: 0,
    },
    {
      tahun: "2025",
      provno: "11",
      kabkotno: "71",
      kodepemda: "1171",
      namapemda: "KOTA BANDA ACEH",
      waktu_mulai: "",
      waktu_selesai: "",
      nama_sub_tahap: "-",
      berlangsung: 0,
    },
    {
      tahun: "2025",
      provno: "11",
      kabkotno: "72",
      kodepemda: "1172",
      namapemda: "KOTA SABANG",
      waktu_mulai: "",
      waktu_selesai: "",
      nama_sub_tahap: "-",
      berlangsung: 0,
    },
    {
      tahun: "2025",
      provno: "11",
      kabkotno: "73",
      kodepemda: "1173",
      namapemda: "KOTA LHOKSEUMAWE",
      waktu_mulai: "",
      waktu_selesai: "",
      nama_sub_tahap: "-",
      berlangsung: 0,
    },
    {
      tahun: "2025",
      provno: "11",
      kabkotno: "74",
      kodepemda: "1174",
      namapemda: "KOTA LANGSA",
      waktu_mulai: "",
      waktu_selesai: "",
      nama_sub_tahap: "-",
      berlangsung: 0,
    },
    {
      tahun: "2025",
      provno: "11",
      kabkotno: "75",
      kodepemda: "1175",
      namapemda: "KOTA SUBULUSSALAM",
      waktu_mulai: "",
      waktu_selesai: "",
      nama_sub_tahap: "-",
      berlangsung: 0,
    },
  ],
});

const rkpdCards = {
  beluminput: { color: "#67B8FF", label: "Belum Input" },
  persiapan: { color: "#1391FF", label: "Persiapan" },
  rancangan: { color: "#1391FF", label: "Rancangan awal" },
  ranwal: { color: "#0070D2", label: "Rancangan" },
  musrenbang: { color: "#005EB0", label: "Musrenbang" },
  rancanganakhir: { color: "#004179", label: "Rancangan Akhir" },
  penetapan: { color: "#002444", label: "Penetapan" },
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
          backgroundColor: ["#67B8FF", "#1391FF", "#0070D2", "#005EB0", "#004179", "#002444", "#4A47FF", "#0300D0", "#00D0E8", "#0097A8"],
          hoverOffset: 4,
        },
      ],
    };

    const chartInstance = new Chart(ctx, {
      type: "pie",
      data: chartData,
      options: {
        responsive: true,
        plugins: {
          legend: {
            position: "right",
            align: "center",
            maxHeight: "1000",
          },
        },
      },
    });
  }
});
</script>

<template>
  <div>
    <div class="flex justify-between items-center">
      <div class="">
        <h1 class="text-2xl text-white">
          {{ $route.params.province.toUpperCase() }}
        </h1>

        <Breadcrumb :province="$route.params.province" :district="$route.params.district" />
      </div>
      <div class="">
        <SelectYear />
      </div>
    </div>

    <div v-if="$route.params.district === 'rekap'">
      <h1>Rekap untuk {{ $route.params.province }}</h1>
      <div class="flex flex-col gap-5 py-5">
        <div class="flex gap-3 flex-col lg:flex-row">
          <div class="bg-[#f9fafb] px-4 sm:px-9 py-3 sm:py-5 lg:p-8 rounded-xl flex flex-col gap-3 text-white w-full">
            <h1 class="text-xl text-white font-semibold mb-2">RKPD</h1>
            <div class="w-full grid grid-cols-2 sm:grid-cols-3 gap-2 sm:gap-5 lg:gap-6 mb-8">
              <StatusCard v-for="(card, key) in rkpdCards" :key="key" :color="card.color" :value="data.singkat[key]" :label="card.label" @card-click="openModal(key)" />
            </div>
          </div>
        </div>
        <div class="flex w-full h-full justify-center bg-[#272B34] rounded p-4 sm:px-20 py-12 max-h-[700px]">
          <canvas id="myChart" class="block"></canvas>
        </div>
        <div></div>
      </div>

      <!-- Modal -->
      <div v-show="showModal" class="absolute top-0 inset-0 bg-black bg-opacity-50 flex items-center justify-center z-[500] py-[10px] overflow-auto">
        <transition name="modal-drop">
          <div v-show="showModal" class="bg-white rounded sm:w-full md:w-3/4 overflow-auto">
            <h2 class="text-2xl bg-[#009efb] p-4 text-white">Detail: {{ selectedCard }}</h2>
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
                        <td class="border border-gray-300 p-2">
                          {{ index + 1 }}
                        </td>
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
    </div>

    <div v-else>
      <div class="w-full bg-white mt-6 rounded">
        <div class="w-full h-16 bg-[#FFBC34] rounded-t text-white p-5 text-xl">
          <h1>Informasi Daerah</h1>
        </div>
        <div class="flex flex-row p-10 items-center">
          <img class="w-28 h-28 mr-10" src="@/assets/images/aceh.png" alt="logo" />
          <div class="flex flex-col w-full">
            <div class="border-b-2 pb-5">
              <h1 class="text-2xl font-medium">
                {{ $route.params.district.toUpperCase() }}
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
    </div>
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
