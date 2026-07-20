<script setup>
const { data: posts } = await useAsyncData('latest-posts', () =>
  queryContent('/blog')
    .sort({ date: -1 })
    .limit(3)
    .find()
)

useSeoMeta({
  title: 'Home | Mohamed Hassanin',
  description: 'Software Engineer, Web Developer, and Technology Enthusiast.',
})
</script>

<template>
  <div class="space-y-24">
    <!-- Hero Section -->
    <section class="grid grid-cols-1 lg:grid-cols-12 gap-12 items-center pt-8">
      <div class="lg:col-span-7 space-y-6 text-left">
        <div class="inline-flex items-center gap-2 px-3 py-1.5 rounded-full bg-indigo-500/10 border border-indigo-500/20 text-indigo-400 text-xs font-semibold tracking-wide">
          <span class="w-2 h-2 rounded-full bg-emerald-400 animate-pulse"></span>
          Software Engineer & Web Developer
        </div>
        <h1 class="text-4xl sm:text-5xl lg:text-6xl font-extrabold tracking-tight text-white leading-none">
          Hello, I'm <span class="text-transparent bg-clip-text bg-gradient-to-r from-indigo-400 via-purple-400 to-pink-500 text-glow-indigo">Mohamed Hassanin</span> 👋🏻
        </h1>
        <p class="text-lg text-zinc-400 max-w-xl leading-relaxed">
          I am a passionate software engineer focused on building robust web applications and API services. I enjoy writing clean code, learning new technologies, and designing elegant solutions.
        </p>
        <div class="flex flex-wrap gap-4">
          <NuxtLink to="/blog" class="inline-flex items-center gap-2 bg-indigo-600 hover:bg-indigo-700 text-white px-6 py-3 rounded-xl font-semibold shadow-lg shadow-indigo-600/20 hover:shadow-indigo-600/35 transition-all duration-300">
            Read My Blog
            <Icon name="lucide:arrow-right" size="1.1rem" />
          </NuxtLink>
          <NuxtLink to="/projects" class="inline-flex items-center gap-2 bg-zinc-900 hover:bg-zinc-800 text-zinc-100 px-6 py-3 rounded-xl font-semibold border border-zinc-800 transition-all">
            View Projects
          </NuxtLink>
        </div>
      </div>
      
      <div class="lg:col-span-5 flex justify-center">
        <div class="relative group">
          <!-- Glow effect background -->
          <div class="absolute -inset-1 rounded-3xl bg-gradient-to-tr from-indigo-500 to-purple-600 opacity-25 blur-xl group-hover:opacity-40 transition-all duration-500"></div>
          <!-- Avatar Frame -->
          <div class="relative glass-panel p-2 rounded-3xl overflow-hidden shadow-2xl">
            <img src="~/assets/images/mohamed-avatar.png" alt="Mohamed Hassanin Avatar" class="w-72 h-72 object-cover rounded-2xl transform group-hover:scale-[1.02] transition duration-500" />
          </div>
        </div>
      </div>
    </section>

    <!-- My Story Section -->
    <section class="space-y-8">
      <div class="text-center max-w-2xl mx-auto space-y-3">
        <h2 class="text-3xl font-bold tracking-tight text-white">My Journey</h2>
        <div class="h-1 w-12 bg-gradient-to-r from-indigo-500 to-purple-500 mx-auto rounded-full"></div>
      </div>

      <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
        <div class="glass-panel p-8 rounded-2xl space-y-4">
          <div class="w-12 h-12 rounded-xl bg-indigo-500/10 border border-indigo-500/20 flex items-center justify-center text-indigo-400">
            <Icon name="lucide:laptop" size="1.5rem" />
          </div>
          <h3 class="text-xl font-semibold text-zinc-50">Software Development</h3>
          <p class="text-zinc-400 text-sm leading-relaxed">
            I am dedicated to crafting clean, maintainable code. I believe in continuous learning and solving complex problems with efficient engineering practices.
          </p>
        </div>

        <div class="glass-panel p-8 rounded-2xl space-y-4">
          <div class="w-12 h-12 rounded-xl bg-purple-500/10 border border-purple-500/20 flex items-center justify-center text-purple-400">
            <Icon name="lucide:share-2" size="1.5rem" />
          </div>
          <h3 class="text-xl font-semibold text-zinc-50">Collaboration</h3>
          <p class="text-zinc-400 text-sm leading-relaxed">
            I enjoy collaborating with developers, sharing technical knowledge, contributing to open source, and discussing modern system architectures.
          </p>
        </div>

        <div class="glass-panel p-8 rounded-2xl space-y-4">
          <div class="w-12 h-12 rounded-xl bg-pink-500/10 border border-pink-500/20 flex items-center justify-center text-pink-400">
            <Icon name="lucide:sparkles" size="1.5rem" />
          </div>
          <h3 class="text-xl font-semibold text-zinc-50">Personal Interests</h3>
          <p class="text-zinc-400 text-sm leading-relaxed">
            Outside of programming, I enjoy reading, exploring new tech developments, and staying active to keep both mind and body energized.
          </p>
        </div>
      </div>
    </section>

    <!-- Latest Blog Posts -->
    <section class="space-y-8">
      <div class="flex items-end justify-between border-b border-zinc-900 pb-4">
        <div>
          <h2 class="text-3xl font-bold tracking-tight text-white">Latest Writing</h2>
          <p class="text-zinc-400 text-sm mt-1">Read my thoughts on programming, architecture, and technology.</p>
        </div>
        <NuxtLink to="/blog" class="group text-indigo-400 hover:text-indigo-300 font-semibold text-sm inline-flex items-center gap-1 transition-all">
          View All Posts
          <Icon name="lucide:arrow-right" size="1rem" class="transform group-hover:translate-x-1 transition-all" />
        </NuxtLink>
      </div>

      <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
        <Post :posts="posts" />
      </div>
    </section>
  </div>
</template>
