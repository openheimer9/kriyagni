<template>
  <section class="py-16 md:py-24 bg-white">
    <div class="container mx-auto px-4">
      <div class="flex flex-col md:flex-row justify-between items-center mb-8 gap-4">
        <!-- Category Filter -->
        <div class="w-full md:w-auto">
          <label for="category" class="sr-only">Filter by Category</label>
          <select id="category" v-model="selectedCategory" class="block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm p-2">
            <option value="">All Categories</option>
            <option v-for="category in uniqueCategories" :key="category" :value="category">{{ category }}</option>
          </select>
        </div>

        <!-- Search Input -->
        <div class="w-full md:w-auto">
          <label for="search" class="sr-only">Search posts</label>
          <input type="text" id="search" v-model="searchTerm" placeholder="Search by title or tag..." class="block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm p-2" />
        </div>
      </div>

      <!-- Featured Post (Optional, if needed) -->
      <!-- <div v-if="featuredPost" class="mb-12">
        <BlogCard :post="featuredPost" class="col-span-full" />
      </div> -->

      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
        <BlogCard v-for="post in paginatedPosts" :key="post.title" :post="post" />
      </div>

      <!-- Pagination -->
      <div v-if="totalPages > 1" class="flex justify-center mt-12 space-x-2">
        <button
          @click="currentPage--"
          :disabled="currentPage === 1"
          class="px-4 py-2 border rounded-md shadow-sm text-sm font-medium"
          :class="currentPage === 1 ? 'bg-gray-200 text-gray-500 cursor-not-allowed' : 'bg-white text-indigo-600 hover:bg-gray-50'"
        >
          Previous
        </button>
        <button
          v-for="page in totalPages"
          :key="page"
          @click="currentPage = page"
          class="px-4 py-2 border rounded-md shadow-sm text-sm font-medium"
          :class="currentPage === page ? 'bg-indigo-600 text-white' : 'bg-white text-gray-700 hover:bg-gray-50'"
        >
          {{ page }}
        </button>
        <button
          @click="currentPage++"
          :disabled="currentPage === totalPages"
          class="px-4 py-2 border rounded-md shadow-sm text-sm font-medium"
          :class="currentPage === totalPages ? 'bg-gray-200 text-gray-500 cursor-not-allowed' : 'bg-white text-indigo-600 hover:bg-gray-50'"
        >
          Next
        </button>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, computed } from 'vue';
import BlogCard from './BlogCard.vue';

const posts = ref([
  {
    title: "The Future of AI-Driven Decision Making",
    author: "Kriyagni AI Team",
    date: "September 15, 2025",
    excerpt: "How prompt engineering is revolutionizing business strategy and execution across industries.",
    category: "AI Strategy",
    image: "/public/images/blog-ai-decision.png",
    tags: ["AI", "Decision Making", "Business Strategy"],
  },
  {
    title: "Automated Workflows: A Complete Guide",
    author: "Kriyagni AI Team",
    date: "September 10, 2025",
    excerpt: "Step-by-step process to implement AI workflows that boost efficiency by 60% or more.",
    category: "Automation",
    image: "/public/images/blog-workflows.jpg",
    tags: ["Automation", "Workflows", "Efficiency"],
  },
  {
    title: "Prompt Systems That Actually Work",
    author: "Kriyagni AI Team",
    date: "September 5, 2025",
    excerpt: "Real-world prompt engineering techniques that deliver measurable results.",
    category: "Prompt Engineering",
    image: "/public/images/blog-prompts.jpg",
    tags: ["Prompts", "AI Systems", "Results"],
  },
  {
    title: "From Complex Problems to Clear Solutions",
    author: "Kriyagni AI Team",
    date: "August 30, 2025",
    excerpt: "How we helped a startup reduce decision-making time by 50% using AI clarity tools.",
    category: "Case Study",
    image: "/public/images/blog-case-study.jpg",
    tags: ["Case Study", "Success Story", "Problem Solving"],
  },
  {
    title: "Building Practical AI for Real Business",
    author: "Kriyagni AI Team",
    date: "August 25, 2025",
    excerpt: "Why practical implementation beats theoretical AI, and how to ensure your AI actually works.",
    category: "Practical AI",
    image: "/public/images/blog-practical-ai.jpg",
    tags: ["Practical AI", "Implementation", "Business Value"],
  },
]);

const selectedCategory = ref('');
const searchTerm = ref('');
const currentPage = ref(1);
const postsPerPage = 6; // You can adjust this value

const filteredPosts = computed(() => {
  let filtered = posts.value;

  if (selectedCategory.value) {
    filtered = filtered.filter(post => post.category === selectedCategory.value);
  }

  if (searchTerm.value) {
    const lowerCaseSearchTerm = searchTerm.value.toLowerCase();
    filtered = filtered.filter(
      post =>
        post.title.toLowerCase().includes(lowerCaseSearchTerm) ||
        post.tags.some(tag => tag.toLowerCase().includes(lowerCaseSearchTerm))
    );
  }

  return filtered;
});

const uniqueCategories = computed(() => {
  const categories = new Set(posts.value.map(post => post.category));
  return Array.from(categories);
});

const totalPages = computed(() => {
  return Math.ceil(filteredPosts.value.length / postsPerPage);
});

const paginatedPosts = computed(() => {
  const start = (currentPage.value - 1) * postsPerPage;
  const end = start + postsPerPage;
  return filteredPosts.value.slice(start, end);
});
</script>