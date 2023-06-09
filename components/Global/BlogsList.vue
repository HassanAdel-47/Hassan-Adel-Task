<template>
  <div>
    <div v-if="blogs.length > 0">
      <div class="flex flex-wrap justify-center">
        <BlogCard v-for="(blog, index) in blogs" :key="index" :blog="blog" />
      </div>
    </div>
    <div v-else>
      <p>No blogs found.</p>
    </div>
  </div>
</template>

<script>
import BlogCard from "./BlogCard.vue";

export default {
  components: { BlogCard },
  props: {
    blogs: {
      type: Array,
      required: true,
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
