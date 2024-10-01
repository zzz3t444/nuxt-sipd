<template>
  <div class="flex flex-col gap-2 w-full">
    <select :name="attr.selectname" :id="attr.selectid" class="hidden" multiple v-model="selected">
      <optgroup v-for="(items, category) in attr.render" :label="category" :key="category">
        <option v-for="item in items" :key="item" class="selectori" :value="item">{{ item }}</option>
      </optgroup>
    </select>
    <div class="w-full relative">
      <span class="button w-[100%] text-white bg-[#323743] rounded-md flex justify-between items-center px-8 py-6 cursor-pointer" @click="toggleDropdown">
        <div>{{ selected.length > 1 ? `${selected.length} dipilih` : (selected.length === 1 ? selected[0] : 'Pilih item') }}</div>
        <i class="fa-solid fa-chevron-down"></i>
      </span>
      <div v-show="isActive" class="w-full bg-[#323743] text-white absolute left-0 top-[100%] z-50 select">
        <div>
          <input type="text" placeholder="Search..." class="search w-full px-4 py-2 border-b-2 bg-[#323743] outline-none" @input="filterItems">
        </div>
        <div class="max-h-[200px] overflow-y-auto no-scrollbar">
          <span class="flex items-center px-4 py-3 hover:bg-blue-500 selectitem" @click="toggleSelectAll">
            <input type="checkbox" :checked="isAllSelected" class="mr-2">Select All
          </span>
          <div v-for="(items, category) in filteredCategories" :key="category">
            <div class="px-4 py-2 font-bold">{{ category }}</div>
            <span v-for="item in items" :key="item" class="flex items-center px-4 py-3 hover:bg-blue-500 selectitem" @click="toggleSelectItem(item)">
              <input type="checkbox" :checked="selected.includes(item)" class="mr-2">{{ item }}
            </span>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts" setup>
const attr = useAttrs()
const selected = ref<string[]>([])
const isActive = ref(false)
const searchQuery = ref('')

// Transform the render prop into a flat list of items for easier filtering
const filteredCategories = computed(() => {
  const result: Record<string, string[]> = {}
  for (const [category, items] of Object.entries(attr.render)) {
    const filteredItems = items.filter((item: string) => item.toLowerCase().includes(searchQuery.value.toLowerCase()))
    if (filteredItems.length > 0) {
      result[category] = filteredItems
    }
  }
  return result
})

const isAllSelected = computed(() => {
  const allItems = Object.values(filteredCategories.value).flat()
  return allItems.length > 0 && allItems.every(item => selected.value.includes(item))
})

const toggleDropdown = () => {
  isActive.value = !isActive.value
}

const filterItems = (event: Event) => {
  searchQuery.value = (event.target as HTMLInputElement).value
}

const toggleSelectItem = (item: string) => {
  if (selected.value.includes(item)) {
    selected.value = selected.value.filter(selectedItem => selectedItem !== item)
  } else {
    selected.value.push(item)
  }
}

const toggleSelectAll = () => {
  const allItems = Object.values(filteredCategories.value).flat()
  if (isAllSelected.value) {
    selected.value = selected.value.filter(item => !allItems.includes(item))
  } else {
    allItems.forEach(item => {
      if (!selected.value.includes(item)) {
        selected.value.push(item)
      }
    })
  }
}

onMounted(() => {
  const handleClickOutside = (event: MouseEvent) => {
    if (!event.target) return
    const targetElement = event.target as HTMLElement
    if (!targetElement.closest('.relative')) {
      isActive.value = false
    }
  }
  window.addEventListener('click', handleClickOutside)
  watch(isActive, (newValue) => {
    if (!newValue) searchQuery.value = ''
  })
})

</script>
