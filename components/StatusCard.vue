<template>
  <div class="card-hover" @click="$emit('cardClick', label)">
    <div
      class="w-full border h-24 p-2 pl-5 rounded-xl flex justify-between bg-white cursor-pointer text-white"
      :style="{
        borderColor: color,
        background: color,
      }"
    >
      <div class="flex flex-col justify-center gap-1">
        <h1 class="text-2xl lg:text-3xl font-semibold">{{ value }}</h1>
        <h1 class="font-medium text-xs">{{ label }}</h1>
      </div>
      <i class="fa-2xl fa-solid fa-chart-simple content-center"></i>
    </div>
  </div>
</template>

<script setup>
defineProps({
  color: {
    type: String,
    default: "#FFFFFF",
  },
  value: {
    type: Number,
    required: true,
  },
  label: {
    type: String,
    required: true,
  },
});

defineEmits(["cardClick"]);
</script>
