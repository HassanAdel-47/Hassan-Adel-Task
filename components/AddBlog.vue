<template>
  <div class="max-w-md mx-auto mt-8 container">
    <h1 class="text-2xl font-bold mb-4">Add New Blog</h1>
    <form @submit.prevent="submitForm">
      <!-- add Author -->
      <div class="mb-4">
        <label for="author" class="block font-bold">Author:</label>
        <input
          type="text"
          v-model="formData.author"
          id="author"
          class="w-full border p-2"
          required
        />
      </div>

      <!-- add Image -->
      <div class="mb-4">
        <label for="image" class="block font-bold">Image:</label>
        <input
          type="file"
          accept="image/*"
          @change="handleImageUpload"
          id="image"
          class="w-full border p-2"
          required
        />
        <img
          class="w-full"
          v-if="formData.image"
          :src="
            formData.image != '' || null
              ? formData.image
              : require('../public/assets/images/blog 1.jpg')
          "
          alt="Blog Image"
        />
      </div>

      <!-- add Title -->
      <div class="mb-4">
        <label for="title" class="block font-bold">Title:</label>
        <input
          v-model.trim="formData.title"
          id="title"
          type="text"
          class="w-full border p-2"
          required
        />
      </div>

      <!-- add Description -->
      <div class="mb-4">
        <label for="description" class="block font-bold">Description:</label>
        <textarea
          v-model.trim="formData.description"
          id="description"
          class="w-full border p-2"
          required
        ></textarea>
      </div>

      <!-- add Category -->
      <div class="mb-4">
        <label for="category" class="block font-bold">Category:</label>
        <select
          id="category"
          v-model="formData.category"
          class="border border-gray-300 px-4 py-2 rounded w-full"
        >
          <option value="">Select a category</option>
          <option
            v-for="category in categories"
            :key="category"
            :value="category"
            required
          >
            {{ category }}
          </option>
        </select>
      </div>

      <!-- add Content -->
      <div class="mb-1">
        <label for="content" class="block font-bold">Content:</label>
        <textarea
          v-model.trim="formData.content"
          id="content"
          class="w-full border p-2 summernote"
          required
        ></textarea>
      </div>
      <div v-if="contentError" class="text-red-500 mb-4">
        Content must be at least 200 characters.
      </div>

      <!-- buttons -->
      <div class="flex justify-center mb-4">
        <nuxt-link
          to="/"
          class="bg-green-500 hover:bg-green-700 text-white font-bold py-2 px-4 mx-2 rounded"
        >
          Back To Blogs
        </nuxt-link>
        <button
          type="submit"
          class="bg-green-500 hover:bg-green-700 text-white font-bold py-2 px-4 mx-2 rounded"
        >
          Add Blog
        </button>
      </div>
    </form>
  </div>
</template>

<script>
import blogsData from "../public/assets/js/blogsData";
export default {
  name: "add-blog",
  data() {
    return {
      formData: {
        title: "",
        author: "",
        category: "",
        description: "",
        content: "",
        image: null,
      },
      contentError: false,
      categories: ["Action", "Technology", "Travel", "Fashion", "Sports"],
    };
  },

  methods: {
    submitForm() {
      const currentDate = new Date();
      const options = { day: "2-digit", month: "2-digit", year: "numeric" };
      const formattedDate = currentDate.toLocaleDateString("en-GB", options);

      if (this.validateForm()) {
        const newBlog = {
          id: Date.now().toString(), //use Variable id for every new Blog
          date: formattedDate, //  current Date in DD-MM-YYYY format
          author: this.formData.author,
          image: this.formData.image,
          title: this.formData.title,
          description: this.formData.description,
          category: this.formData.category,
          content: this.formData.content,
          buttonLabel: "Read More",
        };
        console.log("newBlog:", newBlog);
        blogsData.push(newBlog); // add the new blog to the existing list
        this.$router.push("/"); // redirect Back to the blogs page
      }
    },
    validateForm() {
      // check if content more than 200 char
      if (this.formData.content.length < 200) {
        this.contentError = true;
        return false;
      }
      this.contentError = false;
      return true;
    },

    handleImageUpload(event) {
      // convert image to URL
      const file = event.target.files[0];
      this.formData.image = URL.createObjectURL(file);
    },
  },
};
</script>
