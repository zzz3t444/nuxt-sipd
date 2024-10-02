<script setup>
import { ref, defineAsyncComponent } from "vue";
import { onMounted } from "vue";

const tabs = [
  { name: "RKPD", component: defineAsyncComponent(() => import("./BidangUrusan/TabContent1-bidang.vue")) },
  { name: "RKPD - KUA/PPAS - APBD", component: defineAsyncComponent(() => import("./BidangUrusan/TabContent2-bidang.vue")) },
  { name: "Set Trend", component: defineAsyncComponent(() => import("./BidangUrusan/TabContent3-bidang.vue")) },
];

const activeTab = ref(0);
const fade = ref(false);

onMounted(() => {
  fade.value = true;
});

const switchTab = (index) => {
  fade.value = false;
  setTimeout(() => {
    activeTab.value = index;
    fade.value = true;
  }, 200);
};
</script>

<template>
  <div>
    <div class="flex justify-start space-x-4 border-b-1 mt-10 border-gray-300">
      <div v-for="(tab, index) in tabs" :key="index" class="relative group">
        <button
          :class="['py-2 px-4 flex items-center space-x-2 focus:outline-none', activeTab === index ? 'border-b-4 border-blue-500 text-blue-500' : 'text-gray-500']"
          @mouseenter="switchTab(index)">
          <span>{{ tab.icon }}</span>
          <span>{{ tab.name }}</span>
        </button>

        <div class="absolute left-0 bottom-full mb-2 w-max bg-gray-700 text-white text-xs p-1 rounded hidden group-hover:block">
          {{ tab.name }}
        </div>
      </div>
    </div>

    <transition name="fade" mode="out-in">
      <div class="p-4 pt-0" v-if="fade">
        <component :is="tabs[activeTab].component"></component>
      </div>
    </transition>
  </div>
</template>

<style>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.2s;
}
.fade-enter,
.fade-leave-to {
  opacity: 0;
}
</style>
