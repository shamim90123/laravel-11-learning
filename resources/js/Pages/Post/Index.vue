<template>
    <div class="p-6 bg-gray-100 min-h-screen">
      <h1 class="text-3xl font-bold text-center text-gray-800 mb-6">My Inertia CRUD</h1>

      <div class="text-right mb-4">
        <Link
          href="posts/create"
          class="px-4 py-2 bg-blue-500 text-white rounded shadow hover:bg-blue-600 transition"
        >
          Create New Post
        </Link>
      </div>

      <div class="overflow-x-auto">
        <table class="min-w-full bg-white border rounded-lg shadow">
          <thead>
            <tr class="bg-gray-200 text-gray-700">
              <th
                v-for="header in headers"
                :key="header"
                class="px-4 py-2 text-left font-medium uppercase border-b"
              >
                {{ header }}
              </th>
            </tr>
          </thead>
          <tbody>
            <tr
              v-for="post in posts"
              :key="post.id"
              class="hover:bg-gray-50 transition"
            >
              <td class="px-4 py-2 border-b">{{ post.title }}</td>
              <td class="px-4 py-2 border-b">{{ post.body }}</td>
              <td class="px-4 py-2 border-b flex gap-2">
                <button
                  @click="deletePost(post.slug)"
                  class="px-3 py-1 bg-red-500 text-white rounded shadow hover:bg-red-600 transition"
                >
                  Delete
                </button>
                <Link
                  :href="`posts/${post.slug}/edit`"
                  class="px-3 py-1 bg-green-500 text-white rounded shadow hover:bg-green-600 transition"
                >
                  Edit
                </Link>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </template>

  <script setup>
  import { Link, useForm } from "@inertiajs/vue3";

  defineProps({
    posts: {
      type: Array,
      default: () => [],
    },
  });

  const headers = ["Title", "Body", "Actions"];

  const form = useForm({});

  const deletePost = (id) => {
    form.delete(`posts/${id}`);
  };
  </script>
