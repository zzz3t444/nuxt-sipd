<script setup>
import { ref, onMounted } from "vue";
import { useRoute } from "vue-router";
import temaListData from "../../utils/TematikList.json";

const route = useRoute();
const temaList = temaListData; // Or import it as you did previously
const selectedThemes = ref([]);

onMounted(() => {
  const selectedIds = route.query.selectedIds ? route.query.selectedIds.split(",") : [];
  selectedThemes.value = temaList.filter((theme) => selectedIds.includes(theme.id.toString()));
});
</script>

<template>
  <div>
    <h1 class="text-2xl">Selected Themes</h1>
    <div v-if="selectedThemes.length > 0">
      <ul>
        <li v-for="theme in selectedThemes" :key="theme.id">{{ theme.name }}</li>
      </ul>
    </div>
    <div v-else>
      <p>No themes selected.</p>
    </div>
  </div>
</template>
