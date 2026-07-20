<template>
  <div class="flex flex-col min-h-screen bg-zinc-950 text-zinc-50 selection:bg-indigo-500 selection:text-white antialiased font-sans">
    <!-- Ambient light glow backgrounds -->
    <div class="fixed inset-0 overflow-hidden pointer-events-none z-0">
      <div class="absolute -top-[20%] -left-[20%] w-[70%] h-[70%] rounded-full bg-indigo-600/10 blur-[150px] animate-pulse-slow"></div>
      <div class="absolute -bottom-[20%] -right-[10%] w-[60%] h-[60%] rounded-full bg-purple-600/10 blur-[150px] animate-pulse-slow"></div>
    </div>

    <!-- Header navigation -->
    <SiteHeader class="relative z-50" />

    <!-- Main Content -->
    <main class="mx-auto max-w-7xl px-4 sm:px-6 lg:px-8 grow w-full py-12 relative z-10">
      <slot />
    </main>

    <!-- Footer -->
    <SiteFooter class="relative z-40 mt-auto" />
  </div>
</template>

<style scoped>
.animate-pulse-slow {
  animation: pulse-slow 12s cubic-bezier(0.4, 0, 0.6, 1) infinite;
}
@keyframes pulse-slow {
  0%, 100% { opacity: 0.8; transform: scale(1); }
  50% { opacity: 0.4; transform: scale(1.05); }
}
</style>
