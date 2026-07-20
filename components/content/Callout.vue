<script setup>
const props = defineProps({
  title: {
    type: String,
    default: 'Info'
  }
})
</script>

<template>
  <div class="glass-panel border-l-4 border-l-indigo-500 bg-indigo-500/5 text-zinc-300 p-5 rounded-r-2xl rounded-l-md my-8 shadow-md relative overflow-hidden flex items-start gap-4" role="alert">
    <!-- Ambient glow circle inside -->
    <div class="absolute top-0 left-0 w-24 h-24 rounded-full bg-indigo-500/5 blur-xl -translate-x-6 -translate-y-6"></div>

    <div class="p-1.5 rounded-lg bg-indigo-500/10 border border-indigo-500/20 text-indigo-400 shrink-0">
      <Icon name="lucide:info" size="1.2rem" />
    </div>

    <div class="space-y-1 relative z-10">
      <p class="font-bold text-zinc-100 text-base leading-snug">{{ props.title }}</p>
      <div class="text-zinc-300 text-sm leading-relaxed">
        <slot />
      </div>
    </div>
  </div>
</template>
