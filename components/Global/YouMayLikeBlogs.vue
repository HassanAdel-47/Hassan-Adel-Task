<template>
  <div class="mb-4">
    <h2 class="text-xl font-bold mb-4 mt-2">You May Like</h2>
    <div class="flex flex-wrap justify-center">
      <BlogCard
        v-for="(blog, index) in relatedBlogs"
        :key="index"
        :blog="blog"
      />
    </div>
  </div>
</template>

<script>
import blogsData from "../../public/assets/js/blogsData";
import BlogCard from "./BlogCard.vue";

export default {
  components: { BlogCard },
  props: {
    currentCategory: {
      type: String,
      required: true,
    },
    currentBlogId: {
      type: String,
      required: true,
    },
  },
  computed: {
    relatedBlogs() {
      // bring related blogs based on same category
      return blogsData.filter(
        (blog) =>
          blog.category === this.currentCategory &&
          blog.id !== this.currentBlogId
      );
    },
  },
  methods: {
    getBlogImage(blog) {
      return blog.image !== "" && blog.image !== null
        ? blog.image
        : require("../../public/assets/images/blog 1.jpg");
    },
    limitText(text, limit) {
      if (text && text.length > limit) {
        const truncatedText = text.slice(0, limit);
        const lastSpaceIndex = truncatedText.lastIndexOf(" ");
        if (lastSpaceIndex !== -1) {
          return truncatedText.slice(0, lastSpaceIndex) + "...";
        }
      }
      return text;
    },
  },
};
</script>
