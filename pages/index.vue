<script setup>
import { ref, computed } from "vue";
import { Chart } from "chart.js/auto";
import IndexData from "../utils/indexData.json";
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

const data = ref(IndexData);

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
          hoverOffset: 20,
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
        <h1 class="text-xl text-black font-bold mb-2">RKPD</h1>
        <div class="w-full grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-5 sm:gap-5 lg:gap-3 mb-8">
          <StatusCard
            v-for="(card, key) in rkpdCards"
            :key="key"
            :color="card.color"
            :value="data.singkat[key]"
            class="hover:scale-105 duration-150"
            :label="card.label"
            @card-click="openModal(key)" />
        </div>
      </div>

      <div class="flex flex-col sm:flex-row gap-5 w-full">
        <div class="bg-white px-4 sm:px-9 py-3 sm:py-5 lg:p-8 rounded-3xl flex flex-col gap-3 text-white w-full">
          <h1 class="text-xl text-black font-bold mb-2">KUA dan PPAS</h1>
          <div class="w-full grid grid-cols-1 sm:grid-cols-1 gap-5 sm:gap-5 lg:gap-3 mb-8">
            <StatusCard
              v-for="(card, key) in kuaPpasCards"
              :key="key"
              :color="card.color"
              :value="data.singkat[key]"
              class="hover:scale-105 duration-150"
              :label="card.label"
              @card-click="openModal(key)" />
          </div>
        </div>

        <div class="bg-white px-4 sm:px-9 py-3 sm:py-5 lg:p-8 rounded-3xl flex flex-col gap-3 text-white w-full">
          <h1 class="text-xl text-black font-bold mb-2">APBD</h1>
          <div class="w-full grid grid-cols-1 sm:grid-cols-1 gap-5 sm:gap-5 lg:gap-3 mb-8">
            <StatusCard
              v-for="(card, key) in apbdCards"
              :key="key"
              :color="card.color"
              :value="data.singkat[key]"
              class="hover:scale-105 duration-150"
              :label="card.label"
              @card-click="openModal(key)" />
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
      <div v-show="showModal" class="bg-white rounded-2xl sm:w-full md:w-3/4 overflow-auto">
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
