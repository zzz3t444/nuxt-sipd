<script lang="ts" setup>
import { useAttrs, ref, computed, onMounted, watch } from "vue";

interface Attrs {
  render?: Record<string, string[]>;
  selectname?: string;
  selectid?: string;
}

const attr = useAttrs() as Attrs;

const selected = ref<string[]>([]);
const isActive = ref(false);
const searchQuery = ref("");

const filteredCategories = computed(() => {
  const result: Record<string, string[]> = {};
  const render = attr.render || {};
  for (const [category, items] of Object.entries(render)) {
    if (Array.isArray(items)) {
      const filteredItems = items.filter((item: string) => item.toLowerCase().includes(searchQuery.value.toLowerCase()));
      if (filteredItems.length > 0) {
        result[category] = filteredItems;
      }
    } else {
      console.warn(`Expected items to be an array for category: ${category}`, items);
    }
  }
  return result;
});

const isAllSelected = computed(() => {
  const allItems = Object.values(filteredCategories.value).flat();
  return allItems.length > 0 && allItems.every((item) => selected.value.includes(item));
});

const toggleDropdown = () => {
  isActive.value = !isActive.value;
};

const filterItems = (event: Event) => {
  searchQuery.value = (event.target as HTMLInputElement).value;
};

const toggleSelectItem = (item: string) => {
  if (selected.value.includes(item)) {
    selected.value = selected.value.filter((selectedItem) => selectedItem !== item);
  } else {
    selected.value.push(item);
  }
};

const toggleSelectAll = () => {
  const allItems = Object.values(filteredCategories.value).flat();
  if (isAllSelected.value) {
    selected.value = selected.value.filter((item) => !allItems.includes(item));
  } else {
    allItems.forEach((item) => {
      if (!selected.value.includes(item)) {
        selected.value.push(item);
      }
    });
  }
};

onMounted(() => {
  const handleClickOutside = (event: MouseEvent) => {
    if (!event.target) return;
    const targetElement = event.target as HTMLElement;
    if (!targetElement.closest(".relative")) {
      isActive.value = false;
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
    <select :name="attr.selectname" :id="attr.selectid" class="hidden" multiple v-model="selected">
      <optgroup v-for="(items, category) in filteredCategories" :label="category" :key="category">
        <option v-for="item in items" :key="item" class="selectori" :value="item">{{ item }}</option>
      </optgroup>
    </select>
    <div class="w-full relative">
      <span class="button w-[100%] text-black bg-[#f2f7f8] rounded-md flex justify-between items-center px-8 py-4 cursor-pointer" @click="toggleDropdown">
        <div>{{ selected.length > 1 ? `${selected.length} dipilih` : selected.length === 1 ? selected[0] : "- Belum Memilih - " }}</div>
        <i class="fa-solid fa-chevron-down"></i>
      </span>
      <div v-show="isActive" class="w-full bg-white shadow-xl rounded-lg text-black absolute left-0 top-[100%] z-50 select">
        <div>
          <input type="text" placeholder="Search..." class="search w-full px-4 py-2 border-b-2 bg-[#f2f7f8] outline-none" @input="filterItems" />
        </div>
        <div class="max-h-[200px] overflow-y-auto no-scrollbar">
          <span class="flex items-center px-4 py-3 hover:bg-blue-500 hover:text-white selectitem" @click="toggleSelectAll">
            <input type="checkbox" :checked="isAllSelected" class="mr-2" />Select All
          </span>
          <div v-for="(items, category) in filteredCategories" :key="category">
            <div class="px-4 py-2 font-bold">{{ category }}</div>
            <span v-for="item in items" :key="item" class="flex items-center px-4 py-2 hover:text-white hover:bg-blue-500 selectitem" @click="toggleSelectItem(item)">
              <input type="checkbox" :checked="selected.includes(item)" class="mr-2" />{{ item }}
            </span>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
