<script setup>
const props = defineProps({
  posts: {
    type: Array,
    required: true
  }
})

const formatDate = (dateStr) => {
  if (!dateStr) return '';
  const date = new Date(dateStr);
  return date.toLocaleDateString('en-US', {
    month: 'short',
    day: 'numeric',
    year: 'numeric'
  });
}
</script>

<template>
  <div v-for="post in props.posts" :key="post._path"
    class="glass-panel glass-card-hover rounded-2xl overflow-hidden flex flex-col h-full shadow-lg border border-zinc-800/40">
    
    <NuxtLink :to="post._path" class="block overflow-hidden relative group aspect-video">
      <div class="absolute inset-0 bg-gradient-to-t from-zinc-950/80 via-transparent to-transparent z-10"></div>
      <img :src="`/images/blog/${post.cover}`" :alt="post.title"
        class="w-full h-full object-cover group-hover:scale-105 transition-transform duration-500" />
    </NuxtLink>

    <div class="p-6 flex flex-col grow justify-between space-y-4">
      <div class="space-y-2">
        <div class="flex items-center gap-2 text-xs text-zinc-500 font-medium">
          <Icon name="lucide:calendar" size="0.9rem" />
          <span>{{ formatDate(post.date) }}</span>
          <span class="w-1 h-1 rounded-full bg-zinc-700"></span>
          <Icon name="lucide:clock" size="0.9rem" />
          <span>5 min read</span>
        </div>

        <NuxtLink :to="post._path" class="block group">
          <h3 class="text-xl font-bold text-zinc-100 group-hover:text-indigo-400 transition-colors line-clamp-2 leading-snug">
            {{ post.title }}
          </h3>
        </NuxtLink>
        
        <p class="text-zinc-400 text-sm leading-relaxed line-clamp-3">
          {{ post.description }}
        </p>
      </div>

      <div class="pt-4 border-t border-zinc-900/60 flex items-center justify-between">
        <div class="flex flex-wrap gap-2">
          <span v-for="tag in post.tags?.slice(0, 2)" :key="tag"
            class="text-[10px] uppercase font-bold tracking-wider px-2 py-0.5 rounded-md bg-indigo-500/10 text-indigo-400 border border-indigo-500/20">
            {{ tag }}
          </span>
        </div>
        
        <NuxtLink :to="post._path"
          class="text-xs font-semibold text-zinc-300 hover:text-indigo-400 inline-flex items-center gap-1 transition-colors group">
          Read More
          <Icon name="lucide:arrow-right" size="0.9rem" class="transform group-hover:translate-x-0.5 transition-transform" />
        </NuxtLink>
      </div>
    </div>
  </div>
</template>
