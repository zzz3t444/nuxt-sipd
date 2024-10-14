<script setup>
import { ref } from "vue";

const tabs = [
  { name: "Proporsi Pendanaan", component: defineAsyncComponent(() => import("./TabContent1-tematik.vue")) },
  { name: "Indikator Kerja", component: defineAsyncComponent(() => import("./TabContent2-tematik.vue")) },
  { name: "Set Trend Sub Keg", component: defineAsyncComponent(() => import("./TabContent3-tematik.vue")) },
  { name: "Set Trend Daerah", component: defineAsyncComponent(() => import("./TabContent3-tematik.vue")) },
];

const activeTab = ref(0);
</script>

<template>
  <div>
    <div class="flex justify-start space-x-4 border-b-1 border-gray-300">
      <button
        v-for="(tab, index) in tabs"
        :key="index"
        :class="['py-2 px-4 focus:outline-none', activeTab === index ? 'border-b-4 border-blue-500 text-blue-500' : 'text-gray-500']"
        @click="activeTab = index">
        {{ tab.name }}
      </button>
    </div>

    <div class="pt-0">
      <component :is="tabs[activeTab].component"></component>
    </div>
  </div>
</template>
