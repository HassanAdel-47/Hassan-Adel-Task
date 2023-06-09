<template>
  <div class="flex flex-col w-full">
    <button
      @click="resetCategoryFilter"
      :class="{
        'bg-green-500 text-white': selectedCategory === '',
        'bg-gray-300': selectedCategory !== '',
      }"
      class="mr-2 mb-2 px-4 py-2 rounded hover:bg-green-700 hover:text-white"
    >
      All
    </button>
    <button
      v-for="category in categories"
      :key="category"
      @click="applyCategoryFilter(category)"
      :class="{
        'bg-green-500 text-white': selectedCategory === category,
        'bg-gray-300': selectedCategory !== category,
      }"
      class="mr-2 mb-2 px-4 py-2 rounded hover:bg-green-700 hover:text-white"
    >
      {{ category }}
    </button>
  </div>
</template>

<script>
export default {
  props: {
    selectedCategory: {
      type: String,
      required: true,
    },
    categories: {
      type: Array,
      required: true,
    },
    applyCategoryFilter: {
      type: Function,
      required: true,
    },
    resetCategoryFilter: {
      type: Function,
      required: true,
    },
  },
};
</script>
