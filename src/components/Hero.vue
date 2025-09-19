<template>
  <section class="relative min-h-screen flex items-center justify-center overflow-hidden py-20">
    <!-- Gradient Background -->
    <div class="absolute inset-0 bg-gradient-to-br from-purple-900 via-blue-900 to-gray-900 opacity-90"></div>
    
    <!-- 3D Brain Model -->
    <BrainModel />
    
    <!-- Neural Network Grid -->
    <div class="absolute inset-0" style="background-image: radial-gradient(circle at 1px 1px, rgba(255, 255, 255, 0.1) 1px, transparent 0); background-size: 40px 40px;"></div>
    
    <!-- Floating Particles -->
    <div class="absolute inset-0 overflow-hidden">
      <div v-for="n in 10" :key="n" 
           class="particle absolute rounded-full bg-white"
           :style="getParticleStyle(n)">
      </div>
    </div>

    <!-- Content -->
    <div class="relative container mx-auto px-4 text-center z-10" data-aos="fade-up">
      <h1 class="text-4xl md:text-6xl font-bold mb-6 font-poppins bg-clip-text text-transparent bg-gradient-to-r from-blue-400 to-purple-600 animate-gradient">
        <span v-for="(word, index) in title" :key="index" 
              class="inline-block hover:scale-105 transition-transform duration-300 mx-1"
              :style="{ animationDelay: `${index * 0.1}s` }">
          {{ word }}
        </span>
      </h1>
      <p ref="description" class="text-xl md:text-2xl text-gray-300 mb-12 max-w-3xl mx-auto opacity-0 transform translate-y-4 transition-all duration-1000"
         :class="{ 'opacity-100 translate-y-0': isDescriptionVisible }">
        Transform your business with cutting-edge AI and prompt engineering services that deliver clear, actionable insights.
      </p>
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
import { ref, onMounted } from 'vue';

const title = ['Empowering', 'Decisions', 'with', 'AI', 'Solutions'];
const description = ref<HTMLElement | null>(null);
const isDescriptionVisible = ref(false);

const particles = ref(Array.from({ length: 10 }, (_, i) => ({
  width: (Math.sin(i) * 2 + 2) + 'px',
  height: (Math.sin(i) * 2 + 2) + 'px',
  left: ((i * 10) % 100) + '%',
  top: ((i * 7) % 100) + '%',
  animationDuration: (15 + i * 2) + 's',
  animationDelay: (i * 0.5) + 's'
})));

const getParticleStyle = (n: number) => particles.value[n - 1];

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