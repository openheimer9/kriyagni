<template>
  <section class="relative py-20 overflow-hidden">
    <!-- Neural Network Background -->
    <div class="absolute inset-0 bg-gradient-to-br from-blue-900 to-purple-900">
      <NeuralNetwork />
      <div class="absolute inset-0 bg-gradient-to-t from-transparent via-transparent to-black/30"></div>
    </div>

    <div class="relative container mx-auto px-4 text-center" data-aos="zoom-in">
      <h2 class="text-3xl md:text-5xl font-bold mb-6 text-white font-poppins">
        Ready to Transform Your Business?
      </h2>
      <p class="text-xl text-gray-100 mb-10 max-w-2xl mx-auto">
        Join the AI revolution and stay ahead of the competition with our cutting-edge solutions.
      </p>
      
      <!-- CTA Button with Enhanced Micro-interactions -->
      <button @click="handleClick" 
              @mouseenter="handleHover(true)"
              @mouseleave="handleHover(false)"
              class="relative group inline-flex items-center justify-center">
        <span class="absolute inset-0 rounded-lg bg-gradient-to-r from-blue-500/20 to-purple-500/20 blur-xl transform group-hover:scale-110 transition-all duration-500"></span>
        <span class="absolute inset-0 rounded-lg bg-gradient-to-r from-blue-600/50 to-purple-600/50 opacity-0 group-hover:opacity-100 transition-opacity duration-500"></span>
        <span :class="[isClicked ? 'animate-click' : '', 'relative px-8 py-4 text-lg font-semibold text-white bg-gradient-to-r from-blue-600 to-purple-600 rounded-lg transform transition-all duration-500 group-hover:translate-y-[-2px] group-hover:shadow-[0_0_30px_rgba(88,80,236,0.3)] group-hover:scale-105']">
          <span class="flex items-center justify-center">
            <span :class="['transition-transform duration-500', isHovered ? 'translate-x-[-8px]' : '']">Create It Now</span>
            <svg xmlns="http://www.w3.org/2000/svg" 
                 :class="['h-5 w-5 ml-2 transition-all duration-500', isHovered ? 'translate-x-2 scale-110' : '']"
                 fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 7l5 5m0 0l-5 5m5-5H6" />
            </svg>
          </span>
        </span>
      </button>
    </div>
  </section>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import NeuralNetwork from './NeuralNetwork.vue';

const isClicked = ref(false);
const isHovered = ref(false);

const handleClick = () => {
  isClicked.value = true;
  setTimeout(() => {
    isClicked.value = false;
  }, 200);
};

const handleHover = (hover: boolean) => {
  isHovered.value = hover;
};
</script>

<style scoped>
.animate-click {
  animation: click 200ms cubic-bezier(0.4, 0, 0.2, 1);
}

@keyframes click {
  0% { transform: scale(1); }
  50% { transform: scale(0.95); }
  100% { transform: scale(1); }
}

@keyframes pulse {
  0% { box-shadow: 0 0 0 0 rgba(88, 80, 236, 0.3); }
  70% { box-shadow: 0 0 0 10px rgba(88, 80, 236, 0); }
  100% { box-shadow: 0 0 0 0 rgba(88, 80, 236, 0); }
}
</style>