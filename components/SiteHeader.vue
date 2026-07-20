<script setup>
import { Disclosure, DisclosureButton, DisclosurePanel } from '@headlessui/vue'
import { Bars3Icon, XMarkIcon } from '@heroicons/vue/24/outline'

const route = useRoute();

const navigation = computed(() => [
  { name: 'Home', href: '/', current: route.path === '/' },
  { name: 'Blog', href: '/blog', current: route.path.startsWith('/blog') },
  { name: 'Projects', href: '/projects', current: route.path === '/projects' },
  { name: 'Uses', href: '/uses', current: route.path === '/uses' },
])
</script>

<template>
  <Disclosure as="nav" class="sticky top-0 z-50 glass-panel border-b border-zinc-800/40 backdrop-blur-md bg-zinc-950/70" v-slot="{ open }">
    <div class="mx-auto max-w-7xl px-4 sm:px-6 lg:px-8">
      <div class="relative flex h-16 items-center justify-between">
        
        <div class="absolute inset-y-0 left-0 flex items-center sm:hidden">
          <!-- Mobile menu button-->
          <DisclosureButton
            class="inline-flex items-center justify-center rounded-xl p-2 text-zinc-400 hover:bg-zinc-850 hover:text-zinc-50 focus:outline-none focus:ring-2 focus:ring-inset focus:ring-indigo-500 transition-all">
            <span class="sr-only">Open main menu</span>
            <Bars3Icon v-if="!open" class="block h-6 w-6" aria-hidden="true" />
            <XMarkIcon v-else class="block h-6 w-6" aria-hidden="true" />
          </DisclosureButton>
        </div>

        <div class="flex flex-1 items-center justify-center sm:items-stretch sm:justify-start">
          <NuxtLink to="/" class="flex flex-shrink-0 items-center gap-2 group">
            <div class="h-8 w-8 rounded-lg bg-gradient-to-tr from-indigo-500 to-purple-500 flex items-center justify-center text-white font-extrabold text-sm shadow-md shadow-indigo-500/20 group-hover:scale-105 transition-all">
              MH
            </div>
            <span class="hidden sm:block text-zinc-100 font-bold tracking-tight group-hover:text-indigo-400 transition-all">
              Mohamed Hassanin
            </span>
          </NuxtLink>
          <div class="hidden sm:ml-8 sm:block">
            <div class="flex space-x-1">
              <NuxtLink v-for="item in navigation" :key="item.name" :to="item.href"
                :class="[item.current ? 'bg-indigo-500/10 text-indigo-400 border-indigo-500/20' : 'text-zinc-400 hover:bg-zinc-900 hover:text-zinc-50 border-transparent', 'rounded-xl px-4 py-2 text-sm font-medium border transition-all duration-300']"
                :aria-current="item.current ? 'page' : undefined">{{ item.name }}</NuxtLink>
            </div>
          </div>
        </div>

        <div class="absolute inset-y-0 right-0 flex items-center pr-2 sm:static sm:inset-auto sm:ml-6 sm:pr-0">
          <div class="flex items-center gap-2">
            <a href="https://github.com" target="_blank" rel="noopener noreferrer" class="rounded-full p-2 text-zinc-400 hover:text-zinc-50 hover:bg-zinc-900 transition-all" aria-label="GitHub">
              <Icon name="lucide:github" size="1.25rem" />
            </a>
            <a href="https://twitter.com" target="_blank" rel="noopener noreferrer" class="rounded-full p-2 text-zinc-400 hover:text-zinc-50 hover:bg-zinc-900 transition-all" aria-label="Twitter">
              <Icon name="lucide:twitter" size="1.25rem" />
            </a>
            <a href="https://linkedin.com" target="_blank" rel="noopener noreferrer" class="rounded-full p-2 text-zinc-400 hover:text-zinc-50 hover:bg-zinc-900 transition-all" aria-label="LinkedIn">
              <Icon name="lucide:linkedin" size="1.25rem" />
            </a>
          </div>
        </div>
      </div>
    </div>

    <!-- Mobile Panel -->
    <DisclosurePanel class="sm:hidden border-t border-zinc-800/40 bg-zinc-950/95 backdrop-blur-md">
      <div class="space-y-1 px-3 pb-4 pt-3">
        <DisclosureButton v-for="item in navigation" :key="item.name" as="template">
          <NuxtLink :to="item.href"
            :class="[item.current ? 'bg-indigo-500/10 text-indigo-400 border-indigo-500/20' : 'text-zinc-400 hover:bg-zinc-900 hover:text-zinc-50 border-transparent', 'block rounded-xl px-4 py-2.5 text-base font-medium border transition-all']"
            :aria-current="item.current ? 'page' : undefined">{{ item.name }}</NuxtLink>
        </DisclosureButton>
      </div>
    </DisclosurePanel>
  </Disclosure>
</template>
