<template>
  <div class="bg-white rounded-lg shadow-md hover:shadow-lg transition-shadow duration-300 overflow-hidden">
    <img :src="post.image" :alt="post.title" class="w-full h-48 object-cover" />
    <div class="p-6">
      <div class="flex items-center justify-between text-sm text-gray-500 mb-2">
        <span class="bg-indigo-100 text-indigo-800 px-3 py-1 rounded-full text-xs font-semibold">{{ post.category }}</span>
        <span>{{ post.date }}</span>
      </div>
      <h3 class="text-xl font-bold text-gray-900 mb-2">{{ post.title }}</h3>
      <p class="text-gray-700 text-sm mb-4">{{ post.excerpt }}</p>
      <div class="flex flex-wrap gap-2 mb-4">
        <span v-for="tag in post.tags" :key="tag" class="bg-gray-200 text-gray-700 px-2 py-1 rounded-full text-xs">{{ tag }}</span>
      </div>
      <div class="flex justify-between items-center">
        <a href="#" class="text-indigo-600 hover:text-indigo-800 font-semibold text-sm">Read More</a>
        <div class="flex space-x-2">
          <!-- Social sharing buttons placeholders -->
          <button class="text-gray-400 hover:text-indigo-600"><i class="fab fa-twitter"></i></button>
          <button class="text-gray-400 hover:text-indigo-600"><i class="fab fa-facebook-f"></i></button>
          <button class="text-gray-400 hover:text-indigo-600"><i class="fab fa-linkedin-in"></i></button>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
const props = defineProps({
  post: {
    type: Object,
    required: true,
  },
});
</script>