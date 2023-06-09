<template>
  <div
    class="w-full sm:w-1/2 md:w-1/3 lg:w-1/3 xl:w-1/4 rounded overflow-hidden shadow-lg mx-4 my-2 bg-opacity-25 backdrop-filter backdrop-blur-lg"
    :key="blog.id"
  >
    <img class="w-full" :src="getBlogImage(blog)" alt="Blog Image" />
    <div class="px-6 py-4">
      <p class="text-green-700 text-base">Author: {{ blog.author }}</p>
      <p class="text-gray-700 text-base">Posted in: {{ blog.date }}</p>
      <div class="font-bold text-xl my-1 text-green-500">
        {{ blog.title }}
      </div>
      <p class="text-black text-base">
        {{ blog.description }}
      </p>
      <p class="text-gray-700 text-sm">
        {{ limitText(blog.content, 40) }}
      </p>
    </div>
    <div class="px-6 py-4">
      <nuxt-link
        :to="`/blogs/${blog.id}`"
        class="bg-green-500 hover:bg-green-700 text-white font-bold py-2 px-4 rounded"
      >
        {{ blog.buttonLabel }}
      </nuxt-link>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    blog: {
      type: Object,
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
