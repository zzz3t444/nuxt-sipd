<template>
  <header class="flex items-center mb-5 gap-10">
    <div class="flex items-center gap-4">
      <span>Show</span>
      <select name="entriescount" id="entriescount" class="py-2 px-3 w-[120px] outline-none rounded-md text-left bg-[#f2f7f8]">
        <option value="10">10</option>
        <option value="10">25</option>
        <option value="50">50</option>
        <option value="50">75</option>
        <option value="100" selected>100</option>
      </select>
      <span>Entries</span>
    </div>
    <div class="">
      <span>Showing 0 to 0 of 0 entries</span>
    </div>
  </header>
</template>
