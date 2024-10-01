<script setup>
import { Chart } from "chart.js/auto";
const attr = useAttrs();

onMounted(() => {
  const chart = document.getElementById(`chart${attr.ckey}`);

  if (chart) {
    new Chart(chart, {
      type: "bar",
      data: {
        labels: attr.labels,
        datasets: [
          {
            label: attr.label,
            data: attr.datas,
            borderWidth: 1,
            borderColor: "black",
          },
        ],
      },
      options: {
        borderColor: "black",
        scales: {
          y: {
            beginAtZero: true,
          },
        },
      },
    });
  }
});

const isActive = ref(false);

const activateCollapse = () => {
  isActive.value = !isActive.value;
};
</script>

<template>
  <div :class="`w-full rounded-lg overflow-hidden ${isActive ? '' : 'h-[55px]'} ${attr.bgcolor}`">
    <div class="flex py-4 px-6 justify-between items-center">
      <span>{{ attr.title }}</span>
      <i :class="`fa-solid ${isActive ? 'fa-minus' : 'fa-plus'} cursor-pointer`" v-on:click="activateCollapse"></i>
    </div>
    <div class="p-5">
      <canvas :id="`chart${attr.ckey}`" class="block"></canvas>
    </div>
  </div>
</template>
