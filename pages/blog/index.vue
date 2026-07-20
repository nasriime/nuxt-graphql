<script setup>
const { data: posts } = await useAsyncData('posts', () =>
  queryContent('/blog')
    .sort({ date: -1 })
    .find()
)

useSeoMeta({
  title: 'Blog | Mohamed Hassanin',
  description: 'Articles about Java, Spring Boot, Vue, Nuxt, and modern software engineering.',
})
</script>

<template>
  <div class="space-y-12">
    <!-- Header -->
    <div class="space-y-4 text-left max-w-3xl">
      <h1 class="text-4xl font-extrabold tracking-tight text-white sm:text-5xl">
        Blog Posts
      </h1>
      <p class="text-lg text-zinc-400 leading-relaxed">
        I write about software engineering, developer advocate tips, tutorials, and new tools that catch my interest.
        If you want me to write about a topic or collaborate, feel free to reach out on
        <a href="https://twitter.com" target="_blank" rel="noopener noreferrer" class="text-indigo-400 hover:underline">Twitter</a>.
      </p>
    </div>

    <!-- Post Grid -->
    <section class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
      <Post :posts="posts" />
    </section>
  </div>
</template>
