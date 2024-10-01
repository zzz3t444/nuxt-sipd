<script setup>
const selectedYear = ref("2024");
const years = [2025, 2024, 2023, 2022, 2021, 2020];

const updateYear = () => {
  console.log("Year updated to:", selectedYear.value);
};
</script>

<template>
  <select v-model="selectedYear" @change="updateYear" name="tahun" id="tahun" class="bg-[#f20a34] rounded-full py-2 px-8 text-white font-semibold">
    <option v-for="year in years" :key="year" :value="year" class="bg-white text-black">Tahun {{ year }}</option>
  </select>
</template>
