<template>
    <select v-model="selectedYear" @change="updateYear" name="tahun" id="tahun"
        class="bg-red-600 rounded-full py-2 px-5 text-white font-semibold">
        <option v-for="year in years" :key="year" :value="year" class="bg-white text-black">
            Tahun {{ year }}
        </option>
    </select>
</template>


<script setup>
const selectedYear = ref("2024");
const years = [2025, 2024, 2023, 2022, 2021, 2020];

const updateYear = () => {
    // Here you would typically fetch new data based on the selected year
    // and update data.value accordingly
    console.log("Year updated to:", selectedYear.value);
};

</script>i