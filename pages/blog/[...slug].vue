<script setup>
const { path } = useRoute()

const { data: post } = await useAsyncData(`content-${path}`, () => {
  return queryContent()
    .where({ _path: path })
    .findOne()
})

// Set SEO Meta dynamically
watchEffect(() => {
  if (post.value) {
    useSeoMeta({
      title: `${post.value.title} | Mohamed Hassanin`,
      description: post.value.description,
    })
  }
})

const formatDate = (dateStr) => {
  if (!dateStr) return '';
  const date = new Date(dateStr);
  return date.toLocaleDateString('en-US', {
    month: 'long',
    day: 'numeric',
    year: 'numeric'
  });
}
</script>

<template>
  <div v-if="post" class="max-w-4xl mx-auto space-y-10">
    <!-- Back Navigation -->
    <div>
      <NuxtLink to="/blog" class="inline-flex items-center gap-2 text-zinc-400 hover:text-indigo-400 transition-colors text-sm font-semibold group">
        <Icon name="lucide:arrow-left" size="1.1rem" class="transform group-hover:-translate-x-0.5 transition-transform" />
        Back to Blog
      </NuxtLink>
    </div>

    <!-- Article Header -->
    <header class="space-y-6">
      <div class="flex items-center gap-3 text-sm text-zinc-500 font-medium">
        <Icon name="lucide:calendar" size="1rem" />
        <span>{{ formatDate(post.date) }}</span>
        <span class="w-1 h-1 rounded-full bg-zinc-800"></span>
        <Icon name="lucide:clock" size="1rem" />
        <span>5 min read</span>
      </div>
      
      <h1 class="text-4xl sm:text-5xl font-extrabold tracking-tight text-white leading-tight">
        {{ post.title }}
      </h1>
      
      <p class="text-xl text-zinc-400 leading-relaxed font-light">
        {{ post.description }}
      </p>

      <!-- Cover Image -->
      <div v-if="post.cover" class="relative group rounded-2xl overflow-hidden shadow-2xl border border-zinc-800/40 aspect-[21/9] w-full">
        <img :src="`/images/blog/${post.cover}`" :alt="post.title" class="w-full h-full object-cover" />
      </div>
    </header>

    <!-- Main Content -->
    <main>
      <ContentRenderer :value="post" class="prose prose-zinc prose-invert max-w-none" />
    </main>

    <!-- Tags Footer -->
    <footer class="pt-8 border-t border-zinc-900 flex flex-wrap gap-3">
      <span v-for="tag in post.tags" :key="tag"
        class="inline-flex items-center gap-1.5 text-xs font-semibold px-3 py-1.5 rounded-xl bg-zinc-900 text-zinc-300 border border-zinc-800">
        <Icon name="lucide:tag" size="0.8rem" class="text-zinc-500" />
        {{ tag }}
      </span>
    </footer>
  </div>
</template>
