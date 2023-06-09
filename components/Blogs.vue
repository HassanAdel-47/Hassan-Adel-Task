<template>
  <div>
    <div class="w-full">
      <h1 class="text-4xl text-center font-bold my-4">Blogs</h1>

      <div class="flex flex-col lg:flex-row">
        <div class="w-full lg:w-1/3">
          <!-- Sidebar with categories -->
          <div
            class="bg-gray-100 flex flex-col h-full items-center p-4 rounded"
          >
            <h2 class="text-xl font-bold mb-2">Categories</h2>
            <!-- Category Filter -->
            <CategoryFilter
              :selected-category="selectedCategory"
              :categories="categories"
              :apply-category-filter="applyCategoryFilter"
              :reset-category-filter="resetCategoryFilter"
            />
          </div>
        </div>

        <div class="w-full lg:w-3/4">
          <div class="flex flex-col items-center justify-center">
            <div
              class="flex flex-col justify-content-around items-center lg:flex-row w-100"
            >
              <!-- add new blog button -->
              <nuxt-link
                :to="`/blogs/add-blog`"
                class="bg-green-500 hover:bg-green-700 text-white font-bold py-2 px-4 rounded my-2"
              >
                Add New Blog
              </nuxt-link>

              <!-- Search input field -->
              <input
                type="text"
                v-model="searchQuery"
                placeholder="Search by title or author"
                class="border border-gray-300 px-4 py-2 rounded w-50 my-2"
              />

              <!-- Pagination buttons -->
              <PaginationButtons
                :current-page="currentPage"
                :total-pages="totalPages"
                :go-to-page="goToPage"
              />
            </div>

            <!-- Blog list -->
            <BlogsList :blogs="paginatedBlogs" />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import blogsData from "../public/assets/js/blogsData";
import PaginationButtons from "./Global/PaginationButtons";
import BlogsList from "./Global/BlogsList";
import CategoryFilter from "./Global/CategoryFilter";
export default {
  name: "blogs",
  components: { PaginationButtons, BlogsList, CategoryFilter },
  data() {
    return {
      blogs: blogsData,
      searchQuery: "",
      currentPage: 1,
      blogsPerPage: 3,
      selectedCategory: "",
    };
  },
  methods: {
   
    goToPage(pageNumber) {
      this.currentPage = pageNumber;
    },
    applyCategoryFilter(category) {
      // Apply the selected category filter
      this.selectedCategory = category;
      this.currentPage = 1; // resett current page when changing the category filter
    },
    resetCategoryFilter() {
      // Reset the category filter
      this.selectedCategory = "";
      this.currentPage = 1; // Reset current page when resetting the category filter
    },
  },
  computed: {
    filteredBlogs() {
      // Filter blogs based on search query and selected category
      if (this.searchQuery || this.selectedCategory) {
        const query = this.searchQuery.toLowerCase().trim();
        return blogsData.filter(
          (blog) =>
            (blog.title.toLowerCase().includes(query) ||
              blog.author.toLowerCase().includes(query)) &&
            (this.selectedCategory === "" ||
              blog.category === this.selectedCategory)
        );
      }
      // Return all blogs if no search query or category selected
      return blogsData;
    },
    totalPages() {
      return Math.ceil(this.filteredBlogs.length / this.blogsPerPage);
    },
    paginatedBlogs() {
      const startIndex = (this.currentPage - 1) * this.blogsPerPage;
      const endIndex = startIndex + this.blogsPerPage;
      return this.filteredBlogs.slice(startIndex, endIndex);
    },
    categories() {
      // Get unique categories from blogsData
      const uniqueCategories = new Set(blogsData.map((blog) => blog.category));
      return Array.from(uniqueCategories);
    },
  },
};
</script>
