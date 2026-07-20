<script setup>
const props = defineProps({
  error: Object
})

const handleError = () => clearError({ redirect: '/' })
</script>

<template>
  <div class="flex min-h-screen flex-col items-center justify-center bg-zinc-950 px-4 text-center selection:bg-indigo-500 selection:text-white font-sans relative overflow-hidden">
    <!-- Ambient glows -->
    <div class="absolute inset-0 overflow-hidden pointer-events-none z-0">
      <div class="absolute top-[25%] left-[25%] w-[50%] h-[50%] rounded-full bg-red-900/10 blur-[120px]"></div>
    </div>
    
    <div class="glass-panel max-w-md w-full rounded-2xl p-10 relative z-10 shadow-2xl">
      <div class="text-9xl font-extrabold text-transparent bg-clip-text bg-gradient-to-r from-red-400 to-pink-500 mb-6 drop-shadow-lg">
        {{ error?.statusCode || 'Oops' }}
      </div>
      <h1 class="text-2xl font-bold text-zinc-50 mb-4">
        {{ error?.message || 'Something went wrong.' }}
      </h1>
      <p class="text-zinc-400 mb-8 text-sm leading-relaxed">
        The page you are looking for might have been moved, deleted, or is temporarily unavailable.
      </p>
      <button @click="handleError" class="inline-flex items-center gap-2 bg-gradient-to-r from-indigo-500 to-purple-600 hover:from-indigo-600 hover:to-purple-700 text-white font-semibold px-6 py-3 rounded-xl transition-all duration-300 shadow-lg shadow-indigo-500/20 active:scale-95">
        <Icon name="lucide:home" size="1.2rem" />
        Back to Safety
      </button>
    </div>
  </div>
</template>

<style>
/* Re-declaring the glass-panel class here in case global stylesheet isn't fully loaded */
.glass-panel {
  background: rgba(15, 15, 20, 0.65);
  backdrop-filter: blur(12px);
  -webkit-backdrop-filter: blur(12px);
  border: 1px solid rgba(255, 255, 255, 0.08);
}
</style>
