<template>
  <section class="relative min-h-screen flex items-center justify-center overflow-hidden py-20">
    <!-- Gradient Background -->
    <div class="absolute inset-0 bg-gradient-to-br from-purple-900 via-blue-900 to-gray-900 opacity-90"></div>
    
    <!-- 3D Brain Model -->
    <BrainModel />
    
    <!-- Neural Network Grid -->
    <NeuralNetwork />
    
    <!-- Floating Particles -->
    <FloatingParticles />

    <!-- Content -->
    <div class="relative container mx-auto px-4 text-center z-10" data-aos="fade-up">
      <h1 class="text-6xl md:text-8xl font-extrabold mb-8 font-poppins text-[#E5EAF5] drop-shadow-md animate-text-3d">
      Kriyagni AI
      </h1>
      <h4 class="text-2xl md:text-3xl font-poppins text-[#E5EAF5] drop-shadow-md animate-text-3d mb-8">
  Transform your business with cutting-edge AI and prompt engineering services
  that deliver clear, actionable insights.
</h4>


      <div class="flex flex-col sm:flex-row justify-center gap-6">
        <a href="/login" class="btn-primary">
          Start Now
        </a>
        <a href="/about" class="btn-secondary">
          Learn More
        </a>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import BrainModel from './BrainModel.vue';
import NeuralNetwork from './NeuralNetwork.vue'; // Ensure NeuralNetwork is imported
import FloatingParticles from './FloatingParticles.vue'; // Import the new component
import { ref, onMounted } from 'vue';

const description = ref<HTMLElement | null>(null);
const isDescriptionVisible = ref(false);

onMounted(() => {
  setTimeout(() => {
    isDescriptionVisible.value = true;
  }, 500);
});
</script>

<style scoped>
.btn-primary {
  @apply px-8 py-4 bg-gradient-to-r from-blue-600 to-purple-600 text-white font-semibold rounded-lg
         transform transition-all duration-300 hover:scale-105 hover:shadow-lg;
  position: relative;
  overflow: hidden;
}

.btn-primary::after {
  content: '';
  position: absolute;
  top: -50%;
  left: -50%;
  width: 200%;
  height: 200%;
  background: linear-gradient(45deg, transparent, rgba(255, 255, 255, 0.1), transparent);
  transform: rotate(45deg);
  animation: shine 3s infinite;
}

.btn-secondary {
  @apply px-8 py-4 bg-transparent border-2 border-white text-white font-semibold rounded-lg
         transform transition-all duration-300 hover:bg-white hover:text-gray-900;
}

.animate-text-3d {
  text-shadow: 0 0 10px rgba(139, 92, 246, 0.7), /* Purple */
               0 0 20px rgba(99, 102, 241, 0.5), /* Indigo/Blue */
               0 0 30px rgba(139, 92, 246, 0.3),
               0 0 40px rgba(99, 102, 241, 0.1);
  animation: neon-glow 2s ease-in-out infinite alternate;
}

@keyframes neon-glow {
  from {
    text-shadow: 0 0 5px rgba(139, 92, 246, 0.7),
                 0 0 10px rgba(99, 102, 241, 0.5),
                 0 0 15px rgba(139, 92, 246, 0.3);
  }
  to {
    text-shadow: 0 0 10px rgba(139, 92, 246, 1),
                 0 0 20px rgba(99, 102, 241, 0.8),
                 0 0 40px rgba(139, 92, 246, 0.6),
                 0 0 60px rgba(99, 102, 241, 0.4);
  }
}

.particle {
  opacity: 0.6;
  animation: float linear infinite;
  filter: blur(0px);
  transition: filter 0.3s;
}

.particle:hover {
  filter: blur(2px);
}

@keyframes float {
  0% {
    transform: translateY(0) translateX(0);
    opacity: 0;
  }
  50% {
    opacity: 0.6;
  }
  100% {
    transform: translateY(-100vh) translateX(100px);
    opacity: 0;
  }
}

.animate-gradient {
  background-size: 200% 200%;
  animation: gradient 8s ease infinite;
}

@keyframes gradient {
  0% { background-position: 0% 50%; }
  50% { background-position: 100% 50%; }
  100% { background-position: 0% 50%; }
}

.animate-gradient span {
  animation: fadeInUp 0.5s ease forwards;
  opacity: 0;
  transform: translateY(20px);
}

@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@keyframes shine {
  0% {
    transform: translateX(-100%) rotate(45deg);
  }
  100% {
    transform: translateX(100%) rotate(45deg);
  }
}
</style>