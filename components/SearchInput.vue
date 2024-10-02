<script lang="ts" setup>
interface Attrs {
  searchname?: string;
  searchid?: string;
}

const attr = useAttrs() as Attrs;
</script>

<template>
  <div class="flex w-[350px] bg-[#272B34] rounded-[25px] items-center justify-between gap-3 py-2 px-4 text-white relative">
    <input type="text" :name="attr.searchname" :id="attr.searchid" placeholder="Search..." class="bg-transparent outline-none w-full" />
    <i class="fa-solid fa-search"></i>
  </div>
</template>
