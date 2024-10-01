<template>
  <div class="flex flex-col gap-2 w-full">
    <select :name="attr.selectname" :id="attr.selectid" class="hidden" v-model="selected">
      <option v-for="item in attr.render" :key="item" class="selectori" :value='item'>{{ item }}</option>
    </select>
    <div class="w-full relative">
      <span class="button w-[100%] text-white bg-[#323743] rounded-md flex justify-between items-center px-8 py-6 cursor-pointer" @click="toggleDropdown">
        <div>{{ selected ? selected : 'Pilih item' }}</div>
        <i class="fa-solid fa-chevron-down"></i>
      </span>
      <div v-show="isActive" class="w-full bg-[#323743] text-white absolute left-0 top-[100%] z-50 select">
        <div class="">
          <input type="text" placeholder="Search..." class="search w-full px-4 py-2 border-b-2 bg-[#323743] outline-none" @input="filterItems">
        </div>
        <div class="max-h-[200px] overflow-y-auto no-scrollbar">
          <span v-for="item in filteredItems" :key="item" class="flex flex-col px-4 py-3 hover:bg-blue-500 selectitem" @click="selectItem(item)">{{ item }}</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts" setup>
const attr = useAttrs()
const selected = ref('')
const isActive = ref(false)
const searchQuery = ref('')
const filteredItems = computed(() => {
  return attr.render.filter((item: string) => item.toLowerCase().includes(searchQuery.value.toLowerCase()))
})

const toggleDropdown = () => {
  isActive.value = !isActive.value
}

const filterItems = (event: Event) => {
  searchQuery.value = (event.target as HTMLInputElement).value
}

const selectItem = (item: string) => {
  selected.value = item
  isActive.value = false
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
