<template>
  <section class="relative py-20 bg-gray-900 overflow-hidden">
    <CircuitPattern />
    <div class="container mx-auto px-4 relative z-10">
      <!-- Section Header -->
      <div class="text-center mb-16" data-aos="fade-up">
        <h2 class="text-3xl md:text-4xl font-bold mb-4 font-poppins">
          AI Solutions That Drive Results
        </h2>
        <p class="text-xl text-gray-400 max-w-2xl mx-auto">
          Discover how our AI-powered services can transform your business processes and decision-making.
        </p>
      </div>

      <!-- Service Cards -->
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
        <div v-for="(service, index) in services" :key="index"
             class="group bg-gray-800/80 backdrop-blur-sm rounded-xl p-6 transform transition-all duration-500 hover:scale-105 hover:bg-gray-800/90"
             :data-aos="service.animation"
             :data-aos-delay="service.delay">
          <div class="h-48 mb-6 overflow-hidden rounded-lg bg-gradient-to-br from-purple-500/20 to-blue-500/20 flex items-center justify-center relative">
            <div class="absolute inset-0 bg-gradient-to-br from-purple-600/0 to-blue-600/0 group-hover:from-purple-600/20 group-hover:to-blue-600/20 transition-all duration-500"></div>
            <component :is="service.icon" 
                     class="w-24 h-24 text-blue-500 transform transition-transform duration-500 group-hover:scale-110 group-hover:rotate-12" />
          </div>
          <h3 class="text-xl font-bold mb-3 font-poppins bg-clip-text text-transparent bg-gradient-to-r from-blue-400 to-purple-400">{{ service.title }}</h3>
          <p class="text-gray-400 transition-colors duration-300 group-hover:text-gray-300">{{ service.description }}</p>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { defineComponent, h } from 'vue';
import CircuitPattern from './CircuitPattern.vue';

// Icon components using SVG paths
const BrainIcon = defineComponent({
  render: () => h('svg', {
    xmlns: 'http://www.w3.org/2000/svg',
    fill: 'none',
    viewBox: '0 0 24 24',
    stroke: 'currentColor'
  }, [
    h('path', {
      'stroke-linecap': 'round',
      'stroke-linejoin': 'round',
      'stroke-width': '2',
      d: 'M9.663 17h4.673M12 3v1m6.364 1.636l-.707.707M21 12h-1M4 12H3m3.343-5.657l-.707-.707m2.828 9.9a5 5 0 117.072 0l-.548.547A3.374 3.374 0 0014 18.469V19a2 2 0 11-4 0v-.531c0-.895-.356-1.754-.988-2.386l-.548-.547z'
    })
  ])
});

const AutomationIcon = defineComponent({
  render: () => h('svg', {
    xmlns: 'http://www.w3.org/2000/svg',
    fill: 'none',
    viewBox: '0 0 24 24',
    stroke: 'currentColor'
  }, [
    h('path', {
      'stroke-linecap': 'round',
      'stroke-linejoin': 'round',
      'stroke-width': '2',
      d: 'M4 4v5h.582m15.356 2A8.001 8.001 0 004.582 9m0 0H9m11 11v-5h-.581m0 0a8.003 8.003 0 01-15.357-2m15.357 2H15'
    })
  ])
});

const AnalyticsIcon = defineComponent({
  render: () => h('svg', {
    xmlns: 'http://www.w3.org/2000/svg',
    fill: 'none',
    viewBox: '0 0 24 24',
    stroke: 'currentColor'
  }, [
    h('path', {
      'stroke-linecap': 'round',
      'stroke-linejoin': 'round',
      'stroke-width': '2',
      d: 'M9 19v-6a2 2 0 00-2-2H5a2 2 0 00-2 2v6a2 2 0 002 2h2a2 2 0 002-2zm0 0V9a2 2 0 012-2h2a2 2 0 012 2v10m-6 0a2 2 0 002 2h2a2 2 0 002-2m0 0V5a2 2 0 012-2h2a2 2 0 012 2v14a2 2 0 01-2 2h-2a2 2 0 01-2-2z'
    })
  ])
});

const services = [
  {
    icon: BrainIcon,
    title: 'AI-Powered Solutions',
    description: 'Leverage cutting-edge artificial intelligence to optimize your business processes and decision-making.',
    animation: 'fade-up',
    delay: 0
  },
  {
    icon: AutomationIcon,
    title: 'Workflow Automation',
    description: 'Streamline your operations with intelligent automation that adapts to your business needs.',
    animation: 'fade-up',
    delay: 200
  },
  {
    icon: AnalyticsIcon,
    title: 'Advanced Analytics',
    description: 'Gain valuable insights from your data with our advanced analytics and visualization tools.',
    animation: 'fade-up',
    delay: 400
  }
];
</script>