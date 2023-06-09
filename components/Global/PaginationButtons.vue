<template>
  <div class="flex justify-center my-2">
    <button
      v-for="pageNumber in totalPages"
      :key="pageNumber"
      @click="goToPage(pageNumber)"
      :class="{
        'bg-green-500 hover:bg-green-700 text-white font-bold py-2 px-4 mx-1 rounded h-75':
          currentPage !== pageNumber,
        'bg-green-700 text-white font-bold py-2 px-4 rounded h-75':
          currentPage === pageNumber,
      }"
    >
      {{ pageNumber }}
    </button>
  </div>
</template>

<script>
export default {
  props: {
    currentPage: {
      type: Number,
      required: true,
    },
    totalPages: {
      type: Number,
      required: true,
    },
    goToPage: {
      type: Function,
      required: true,
    },
  },
};
</script>
