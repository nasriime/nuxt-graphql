<script setup>
const links = [
  { name: 'GitHub', href: 'https://github.com', icon: 'lucide:github' },
  { name: 'Twitter', href: 'https://twitter.com', icon: 'lucide:twitter' },
  { name: 'LinkedIn', href: 'https://www.linkedin.com', icon: 'lucide:linkedin' },
  { name: 'Instagram', href: 'https://instagram.com', icon: 'lucide:instagram' }
]
const currentYear = new Date().getFullYear();
</script>

<template>
  <footer class="border-t border-zinc-900/60 bg-zinc-950/40 py-8 mt-20">
    <div class="mx-auto max-w-7xl px-4 sm:px-6 lg:px-8 flex flex-col sm:flex-row items-center justify-between gap-4 text-zinc-400 text-sm">
      <div class="flex items-center gap-2">
        <div class="h-6 w-6 rounded-md bg-gradient-to-tr from-indigo-500 to-purple-500 flex items-center justify-center text-white font-extrabold text-xs">
          MH
        </div>
        <p>&copy; {{ currentYear }} Mohamed Hassanin. All Rights Reserved.</p>
      </div>
      <div class="flex items-center gap-2">
        <a v-for="link in links" :key="link.name" :href="link.href" target="_blank" rel="noopener noreferrer"
          class="rounded-full p-2 text-zinc-400 hover:text-zinc-50 hover:bg-zinc-900 transition-all" :title="link.name">
          <Icon :name="link.icon" size="1.2rem" />
        </a>
      </div>
    </div>
  </footer>
</template>
