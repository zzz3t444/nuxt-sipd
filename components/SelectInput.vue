<script lang="ts" setup>
import { useAttrs, ref, computed, onMounted, watch } from "vue";

interface Attrs {
  render?: string[];
  selectname?: string;
  selectid?: string;
}

const attr = useAttrs() as Attrs;
const selected = ref<string>("");
const isActive = ref(false);
const searchQuery = ref("");
const activeDropdown = ref<number | null>(null);

const filteredItems = computed(() => {
  if (Array.isArray(attr.render)) {
    return attr.render.filter((item) => {
      return typeof item === "string" && item.toLowerCase().includes(searchQuery.value.toLowerCase());
    });
  }
  return [];
});

const toggleDropdown = (index: number) => {
  if (activeDropdown.value === index) {
    isActive.value = !isActive.value;
  } else {
    // Close the previously open dropdown and open the new one
    isActive.value = true;
    activeDropdown.value = index;
  }
};

const filterItems = (event: Event) => {
  searchQuery.value = (event.target as HTMLInputElement).value;
};

const selectItem = (item: string) => {
  selected.value = item;
  isActive.value = false;
  activeDropdown.value = null;
};

onMounted(() => {
  const handleClickOutside = (event: MouseEvent) => {
    if (!event.target) return;
    const targetElement = event.target as HTMLElement;
    if (!targetElement.closest(".relative")) {
      isActive.value = false;
      activeDropdown.value = null;
    }
  };

  window.addEventListener("click", handleClickOutside);
  watch(isActive, (newValue) => {
    if (!newValue) searchQuery.value = "";
  });
});
</script>

<template>
  <div class="flex flex-col gap-2 w-full">
    <select :name="attr.selectname" :id="attr.selectid" class="hidden" v-model="selected">
      <option v-for="item in attr.render" :key="item" class="selectori" :value="item">{{ item }}</option>
    </select>
    <div class="w-full relative">
      <span class="button w-[100%] text-black bg-[#f2f7f8] rounded-md flex justify-between items-center px-8 py-4 cursor-pointer" @click="toggleDropdown(0)">
        <div>{{ selected ? selected : "- Belum Memilih -" }}</div>
        <i class="fa-solid fa-chevron-down"></i>
      </span>
      <div v-show="activeDropdown === 0 && isActive" class="w-full bg-white shadow-xl rounded-lg text-black absolute left-0 top-[100%] z-20 select">
        <div class="">
          <input type="text" placeholder="Search..." class="search w-full px-4 py-2 border-b-2 bg-[#f2f7f8] outline-none" @input="filterItems" />
        </div>
        <div class="max-h-[200px] overflow-y-auto no-scrollbar">
          <span v-for="item in filteredItems" :key="item" class="flex flex-col px-4 py-2 hover:text-white hover:bg-blue-500 selectitem" @click="selectItem(item)">{{ item }}</span>
        </div>
      </div>
    </div>
  </div>
</template>
