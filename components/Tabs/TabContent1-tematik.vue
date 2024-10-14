<script lang="ts">
import { ref, onMounted } from "vue";
import { Chart, BarElement, CategoryScale, LinearScale } from "chart.js";

Chart.register(BarElement, CategoryScale, LinearScale);

export default {
  setup() {
    const fundingChart = ref<HTMLCanvasElement | null>(null);
    const blueChart = ref<HTMLCanvasElement | null>(null);
    const isOrangeOpen = ref(false);
    const isBlueOpen = ref(false);
    let fundingChartInstance: Chart | null = null;
    let blueChartInstance: Chart | null = null;

    const toggleOrange = () => {
      isOrangeOpen.value = !isOrangeOpen.value;
      if (isOrangeOpen.value) {
        isBlueOpen.value = false;
        if (!fundingChartInstance) {
          createFundingChart();
        }
      }
    };

    const toggleBlue = () => {
      isBlueOpen.value = !isBlueOpen.value;
      if (isBlueOpen.value) {
        isOrangeOpen.value = false;
        if (!blueChartInstance) {
          createBlueChart();
        }
      }
    };

    const createFundingChart = () => {
      const ctx = fundingChart.value?.getContext("2d");
      if (ctx) {
        fundingChartInstance = new Chart(ctx, {
          type: "bar",
          data: {
            labels: [
              "Penyusunan Rencana, Kebijakan ...",
              "Supervisi Pembangunan Tingkat ...",
              "Pembangunan Baru SPAM Jaringan ...",
              "Peningkatan SPAM Jaringan Perpip...",
              "Petugas SPAM Jaringan Perpip...",
              "Perbaikan SPAM Jaringan Perpip...",
              "Fasilitas Kerja Sama Pengelola...",
              "Pembinaan Teknis SDM dan Kelemb...",
              "Operasi dan Pemeliharaan SPAM ...",
              "Survei dan Investigasi Untuk Pe...",
              "Penyediaan Lahan untuk Pengemb...",
              "Pembentukan Organisasi Pengel...",
              "Koordinasi, Sinkronisasi, Moni...",
            ],
            datasets: [
              {
                label: "Proporsi Pendanaan",
                data: [3.9, 0.3, 0.6, 0.7, 0.4, 0.65, 0.1, 0.15, 0.2, 0.05, 0.35, 0.2, 0.25],
                backgroundColor: [
                  "rgba(91, 55, 183, 0.8)",
                  "rgba(244, 114, 182, 0.8)",
                  "rgba(132, 245, 141, 0.8)",
                  "rgba(91, 55, 183, 0.8)",
                  "rgba(244, 114, 182, 0.8)",
                  "rgba(91, 55, 183, 0.8)",
                  "rgba(91, 55, 183, 0.8)",
                  "rgba(91, 55, 183, 0.8)",
                  "rgba(244, 114, 182, 0.8)",
                  "rgba(132, 245, 141, 0.8)",
                  "rgba(91, 55, 183, 0.8)",
                  "rgba(91, 55, 183, 0.8)",
                  "rgba(244, 114, 182, 0.8)",
                ],
              },
            ],
          },
          options: {
            responsive: true,
            maintainAspectRatio: false,
            scales: {
              y: {
                beginAtZero: true,
                max: 1,
              },
            },
            plugins: {
              legend: {
                display: false,
              },
            },
          },
        });
      }
    };

    const createBlueChart = () => {
      const ctx = blueChart.value?.getContext("2d");
      if (ctx) {
        blueChartInstance = new Chart(ctx, {
          type: "bar",
          data: {
            labels: ["Example Data 1", "Example Data 2", "Example Data 3"],
            datasets: [
              {
                label: "Proporsi Pendanaan",
                data: [0.5, 0.7, 0.3],
                backgroundColor: ["rgba(54, 162, 235, 0.8)", "rgba(255, 99, 132, 0.8)", "rgba(75, 192, 192, 0.8)"],
              },
            ],
          },
          options: {
            responsive: true,
            maintainAspectRatio: false,
            scales: {
              y: {
                beginAtZero: true,
                max: 1,
              },
            },
            plugins: {
              legend: {
                display: false,
              },
            },
          },
        });
      }
    };

    onMounted(() => {});

    return { fundingChart, blueChart, isOrangeOpen, isBlueOpen, toggleOrange, toggleBlue };
  },
};
</script>

<template>
  <div class="flex flex-col items-center">
    <h2 class="text-center text-lg font-semibold mb-7 mt-5">Proyeksi Pendanaan Per Tingkatan Pemerintah Daerah</h2>

    <!-- Top Dropdown Header -->
    <div class="w-full bg-orange-500 rounded-lg py-4 px-4 text-white text-center flex justify-between items-center cursor-pointer" @click="toggleOrange">
      <span>Provinsi</span>
      <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4" fill="none" viewBox="0 0 24 24" stroke="currentColor">
        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7" />
      </svg>
    </div>

    <!-- Chart Container -->
    <div class="w-full border-2 border-orange-500 rounded-bl-lg rounded-br-lg bg-white p-4" v-show="isOrangeOpen">
      <div class="canvas-container" :class="{ 'h-[700px]': isOrangeOpen, 'h-[300px]': !isOrangeOpen }">
        <canvas ref="fundingChart"></canvas>
      </div>
    </div>

    <!-- Bottom Dropdown Footer -->
    <div class="w-full bg-blue-400 rounded-lg p-2 py-4 px-4 text-white text-center mt-4 flex justify-between items-center cursor-pointer" @click="toggleBlue">
      <span>Provinsi</span>
      <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4" fill="none" viewBox="0 0 24 24" stroke="currentColor">
        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7" />
      </svg>
    </div>

    <!-- Chart Container for Blue Section -->
    <div class="w-full border-2 border-blue-500 rounded-bl-lg rounded-br-lg bg-white p-4" v-show="isBlueOpen">
      <div class="canvas-container" :class="{ 'h-[700px]': isBlueOpen, 'h-[300px]': !isBlueOpen }">
        <canvas ref="blueChart"></canvas>
      </div>
    </div>
  </div>
</template>

<style scoped>
.canvas-container {
  transition: height 0.3s ease-in-out;
  height: 600px;
}
</style>
