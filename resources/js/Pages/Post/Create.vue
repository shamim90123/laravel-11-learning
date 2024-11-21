<template>
    <div class="p-6 max-w-lg mx-auto bg-white rounded-lg shadow-lg">
      <form @submit.prevent="submit" class="space-y-4">
        <div>
          <label
            for="title"
            class="block text-sm font-medium text-gray-700"
          >
            Title
          </label>
          <input
            type="text"
            id="title"
            v-model="form.title"
            class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:ring-blue-500 focus:border-blue-500 sm:text-sm"
            placeholder="Enter post title"
          />
        </div>

        <div>
          <label
            for="body"
            class="block text-sm font-medium text-gray-700"
          >
            Body
          </label>
          <textarea
            id="body"
            v-model="form.body"
            class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:ring-blue-500 focus:border-blue-500 sm:text-sm"
            rows="4"
            placeholder="Enter post body"
          ></textarea>
        </div>

        <div class="flex justify-end">
          <button
            type="submit"
            class="px-4 py-2 bg-blue-500 text-white rounded-md shadow hover:bg-blue-600 focus:outline-none focus:ring focus:ring-blue-300 transition"
          >
            {{ props.isUpdating ? "Update" : "Submit" }}
          </button>
        </div>
      </form>
    </div>
  </template>

  <script setup>
  import { onMounted } from "vue";
  import { useForm } from "@inertiajs/vue3";

  const props = defineProps({
    post: {
      type: Object,
      default: null,
    },
    isUpdating: {
      type: Boolean,
      default: false,
    },
  });

  const form = useForm({
    title: "",
    body: "",
  });

  const submit = () => (props.isUpdating ? updatePost() : addPost());
  const addPost = () => form.post("/posts");
  const updatePost = () => form.put(`/posts/${props.post.id}`);

  onMounted(() => {
    if (props.post) {
      form.title = props.post.title;
      form.body = props.post.body;
    }
  });
  </script>

  <style lang="scss" scoped>
  /* You can add additional styles here if needed */
  </style>
