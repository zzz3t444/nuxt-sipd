<script>
export default {
  props: {
    province: {
      type: String,
      default: "",
    },
    district: {
      type: String,
      default: "",
    },
  },
};
</script>

<template>
  <nav class="flex flex-row items-center text-sm text-neutral-500">
    <NuxtLink to="/" class="mr-2 text-[#009efb] hover:text-[#7460e]">Dashboard</NuxtLink>
    <span v-if="province" class="mr-2">></span>
    <h1 v-if="province" class="breadcrumb-item" :class="{ active: !district }">
      <template v-if="district">
        <NuxtLink :to="`/dashboard/${province}`" class="mr-2 text-[#009efb] hover:text-[#7460e]">
          {{ province.toUpperCase() }}
        </NuxtLink>
      </template>
      <template v-else>{{ province.toUpperCase() }}</template>
    </h1>
    <span v-if="district" class="mr-2">></span>
    <div v-if="district" class="breadcrumb-item active">{{ district }}</div>
  </nav>
</template>
