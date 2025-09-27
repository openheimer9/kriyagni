<template>
  <section class="relative min-h-[60vh] flex items-center justify-center overflow-hidden bg-gradient-to-br from-gray-900 via-purple-900 to-blue-900">
    <div class="absolute inset-0 bg-[radial-gradient(circle_at_30%_50%,rgba(56,189,248,0.1),transparent_50%)]" />
    <div class="absolute inset-0 bg-[radial-gradient(circle_at_70%_50%,rgba(168,85,247,0.1),transparent_50%)]" />
    
    <div class="container mx-auto px-4 py-20 text-center relative z-10">
      <h1 class="text-5xl md:text-6xl font-bold text-white mb-6 font-poppins bg-clip-text text-transparent bg-gradient-to-r from-blue-400 to-purple-400">
        Smart Solutions
      </h1>
      <p class="text-xl md:text-2xl text-gray-300 max-w-3xl mx-auto font-inter">
        Transforming complex problems into clear, actionable AI solutions.
      </p>
    </div>

    <!-- Animated Background Pattern -->
    <div class="absolute inset-0 opacity-20">
      <div class="absolute inset-0 bg-grid-pattern animate-grid-flow"></div>
    </div>
  </section>
</template>

<style scoped>
.bg-grid-pattern {
  background-size: 50px 50px;
  background-image: linear-gradient(to right, rgba(255,255,255,0.1) 1px, transparent 1px),
                    linear-gradient(to bottom, rgba(255,255,255,0.1) 1px, transparent 1px);
}

@keyframes grid-flow {
  0% {
    transform: translateY(0);
  }
  100% {
    transform: translateY(50px);
  }
}

.animate-grid-flow {
  animation: grid-flow 20s linear infinite;
}
</style>