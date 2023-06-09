<template>
  <div v-if="blog" class="container">
    <h1 class="text-4xl text-green-500 font-bold my-4 text-center">
      {{ blog.title }}
    </h1>
    <div class="flex items-center justify-center w-100">
      <img
        :src="
          blog.image != '' || null
            ? blog.image
            : require('../public/assets/images/blog 1.jpg')
        "
        alt="Blog Image"
        class="mb-4 w-full md:w-1/3"
      />
    </div>
    <p class="text-base mb-2 text-green-500">By: {{ blog.author }}</p>
    <p class="text-gray-700 text-base mb-2">Posted in: {{ blog.date }}</p>
    <p class="text-gray-700 text-base mb-4">{{ blog.description }}</p>
    <p class="text-gray-700 text-base mb-4">{{ blog.content }}</p>
    <nuxt-link
      to="/"
      class="bg-green-500 hover:bg-green-700 text-white font-bold py-2 px-4 mx-2 my-2 rounded"
    >
      Back To Blogs
    </nuxt-link>
    <hr class="mt-5 bg-green-500" />
    <YouMayLike :currentCategory="blog.category" :currentBlogId="blog.id" />
  </div>
</template>

<script>
import blogsData from "../public/assets/js/blogsData";
import YouMayLike from "./Global/YouMayLikeBlogs.vue";
export default {
  name: "blog-details",
  components: { YouMayLike },
  data() {
    return {
      blog: null,
      blogsData: "",
    };
  },
  mounted() {
    const blogId = this.$route.params.id;
    this.blog = blogsData.find((myblog) => myblog.id === blogId);
  },
};
</script>
