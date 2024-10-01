<template>
  <p>Page visits: {{ count }}</p>
</template>

<script setup lang="ts">
const { data: count } = await useFetch(
  "https://cdn.kotakpasir.dev/edb-gis/2024%2Fdetail_status_rkpd_perkab_kota.json"
);
</script>
