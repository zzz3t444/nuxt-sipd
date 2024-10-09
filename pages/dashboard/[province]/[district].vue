<script setup>
import { onMounted, ref, computed } from "vue";
import { Chart } from "chart.js/auto";
import StatusCard from "../components/StatusCard.vue";
import DistricData from "../../../utils/district.json";

const searchTerm = ref("");

const filteredData = computed(() => {
  if (!searchTerm.value) return selectedData.value;
  return selectedData.value.filter(
    (item) =>
      item.namapemda.toLowerCase().includes(searchTerm.value.toLowerCase()) || item.kodepemda.includes(searchTerm.value) || item.nama_sub_tahap.toLowerCase().includes(searchTerm.value.toLowerCase())
  );
});

const data = ref(DistricData);

const rkpdCards = {
  beluminput: { color: "#ff2f55", label: "Belum Input" },
  persiapan: { color: "#f54eb9", label: "Persiapan" },
  rancangan: { color: "#39c449", label: "Rancangan Awal" },
  ranwal: { color: "#263238", label: "Rancangan" },
  musrenbang: { color: "#ffbc34", label: "Musrenbang" },
  rancanganakhir: { color: "#7460ee", label: "Rancangan Akhir" },
  penetapan: { color: "#009efb", label: "Penetapan" },
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
          backgroundColor: ["#ef4444", "#22c55e", "#1f2937", "#eab308", "#9333ea", "#3b82f6", "#c084fc"],
          hoverOffset: 10,
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
        <h1 class="text-2xl text-black">
          {{ $route.params.province.toUpperCase() }}
        </h1>

        <Breadcrumb :province="$route.params.province" :district="$route.params.district" />
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
        <img class="w-52 h-52 mr-10" src="@/assets/images/aceh.png" alt="logo" />
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

    <div class="text-lg w-full py-3 px-5 mt-10 bg-[#ccecfe] text-[#5E5E5E] border border-[#b8e4fe] rounded-md">
      <div class="">
        Posisi Per-Provinsi Tahun:
        <b class="text-black">{{ data.singkat.tahun }}</b>
      </div>
    </div>

    <div v-if="$route.params.district === 'rekap'">
      <!-- <h1>Rekap untuk {{ $route.params.province }}</h1> -->
      <div class="flex flex-col gap-5 py-5">
        <div class="flex gap-3 flex-col lg:flex-row">
          <div class="bg-white px-4 sm:px-9 py-3 sm:py-5 lg:p-8 rounded-3xl flex flex-col gap-3 text-black w-full">
            <h1 class="text-xl font-semibold mb-2">RKPD</h1>
            <div class="w-full grid grid-cols-1 sm:grid-cols-2 md:grid-cols-4 lg:grid-cols-7 gap-3 mb-8">
              <StatusCard
                v-for="(card, key) in rkpdCards"
                :key="key"
                :color="card.color"
                :value="data.singkat[key]"
                :label="card.label"
                @card-click="openModal(key)"
                class="w-full hover:scale-105 duration-150 hover:shadow-md" />
            </div>
          </div>
        </div>

        <!-- Bottom Row with 3 Grids -->
        <div class="flex w-full justify-center bg-white rounded-3xl sm:px-20">
          <div class="w-[700px] grid sm:grid-cols-3 gap-5">
            <canvas id="myChart" class="col-span-3" width="600" height="400"></canvas>
          </div>
        </div>
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
