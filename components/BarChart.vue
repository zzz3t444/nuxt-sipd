<script>
import { ref, onMounted } from "vue";
import { Chart, BarElement, CategoryScale, LinearScale } from "chart.js";

Chart.register(BarElement, CategoryScale, LinearScale);

export default {
  name: "FundingChart",
  setup() {
    const fundingChart = ref(null);

    onMounted(() => {
      const ctx = fundingChart.value.getContext("2d");
      new Chart(ctx, {
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
              data: [0.9, 0.5, 0.4, 0.65, 0.35, 0.75, 0.25, 0.45, 0.1, 0.15, 0.05, 0.2, 0.15],
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
    });

    return { fundingChart };
  },
};
</script>

<template>
  <div class="flex flex-col items-center">
    <h2 class="text-center text-lg font-semibold mb-4">Proyeksi Pendanaan Per Tingkatan Pemerintah Daerah</h2>
    <div class="w-full md:w-3/4 lg:w-2/3 bg-orange-500 rounded-t-lg p-2 text-white text-center">Provinsi</div>
    <div class="w-full md:w-3/4 lg:w-2/3 border-t-2 border-orange-500 p-4 bg-white">
      <canvas ref="fundingChart"></canvas>
    </div>
    <div class="w-full md:w-3/4 lg:w-2/3 bg-blue-400 rounded-b-lg p-2 text-white text-center mt-2">Provinsi</div>
  </div>
</template>

<style scoped>
.canvas-container {
  height: 400px;
}
</style>
