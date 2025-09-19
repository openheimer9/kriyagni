<script setup>
import promptSystems from '../images/prompt-systems.jpg';
import automatedWorkflows from '../images/automated-workflows.jpg';
import clarityBoost from '../images/clarity-boost.jpg';
import practicalAi from '../images/practical-ai.jpg';

const solutions = [
  {
    title: "Prompt Systems",
    description: "Enhancing strategy and decision-making with AI-driven prompts.",
    image: promptSystems
  },
  {
    title: "Automated Workflows",
    description: "Streamlining operations to boost efficiency and execution speed.",
    image: automatedWorkflows
  },
  {
    title: "Clarity Boost",
    description: "Helping teams achieve clarity and confidence in decisions.",
    image: clarityBoost
  },
  {
    title: "Practical AI",
    description: "Making AI useful for real-world business challenges.",
    image: practicalAi
  }
];
</script>

<template>
  <div class="py-20 bg-gray-900">
    <div class="container mx-auto px-4">
      <div class="grid grid-cols-1 sm:grid-cols-2 gap-6 sm:gap-8 max-w-6xl mx-auto">
        <div v-for="solution in solutions" :key="solution.title"
             class="group relative bg-gray-800 rounded-xl overflow-hidden transition-transform duration-300 hover:transform hover:scale-[1.02] hover:shadow-2xl">
          <div class="relative aspect-[16/9] overflow-hidden">
            <img :src="solution.image.src" :alt="solution.title"
                 class="absolute inset-0 w-full h-full object-cover object-center transform transition-transform duration-500 group-hover:scale-110" />
          </div>

          <div class="p-6 relative">
            <div class="absolute inset-0 bg-gradient-to-t from-gray-900/90 to-transparent opacity-0 group-hover:opacity-100 transition-opacity duration-300"></div>

            <h3 class="text-2xl font-bold text-white mb-3 font-poppins relative z-10 group-hover:text-blue-400 transition-colors duration-300">
              {{ solution.title }}
            </h3>
            <p class="text-gray-300 relative z-10 group-hover:text-white transition-colors duration-300">
              {{ solution.description }}
            </p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>