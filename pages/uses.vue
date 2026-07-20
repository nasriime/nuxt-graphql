<script setup>
const techStack = [
  { name: 'Vue 3', icon: 'logos:vue', href: 'https://vuejs.org/', desc: 'Progressive JavaScript framework for user interfaces.' },
  { name: 'Nuxt 3', icon: 'logos:nuxt-icon', href: 'https://nuxt.com/', desc: 'Intuitive Vue framework for build-ready production apps.' },
  { name: 'Tailwind CSS', icon: 'logos:tailwindcss-icon', href: 'https://tailwindcss.com/', desc: 'A utility-first CSS framework for rapid UI styling.' },
  { name: 'Netlify', icon: 'logos:netlify-icon', href: 'https://netlify.com/', desc: 'Hosting platform for automated git deployments & CDN.' }
]

const editorSetup = [
  { name: 'VS Code', icon: 'logos:visual-studio-code', href: 'https://code.visualstudio.com/', desc: 'Primary code editor loaded with productivity extensions.' },
  { name: 'Synthwave 84', icon: 'lucide:palette', href: 'https://marketplace.visualstudio.com/items?itemName=RobbOwen.synthwave-vscode', desc: 'VS Code theme by Robb Owen with neon glowing effects.' },
  { name: 'Hack Font', icon: 'lucide:type', href: 'https://sourcefoundry.org/hack/', desc: 'Monospaced typeface designed specifically for source code.' },
  { name: 'iTerm2', icon: 'lucide:terminal', href: 'https://www.iterm2.com/', desc: 'Highly customizable terminal emulator replacement for macOS.' }
]

useSeoMeta({
  title: 'Uses | Dan Vega',
  description: 'The software, hardware, and setup gear used by Dan Vega.',
})
</script>

<template>
  <div class="space-y-16">
    <!-- Header -->
    <div class="space-y-4 text-left max-w-3xl">
      <h1 class="text-4xl font-extrabold tracking-tight text-white sm:text-5xl">
        Uses
      </h1>
      <p class="text-lg text-zinc-400 leading-relaxed">
        I am often asked about the software, gear, and developer environment I use as a content creator and advocate.
        This is a living document of my current workspace tools.
        If you have questions, reach out on
        <a href="https://twitter.com" target="_blank" rel="noopener noreferrer" class="text-indigo-400 hover:underline">Twitter</a>.
      </p>
    </div>

    <!-- Tech Stack Category -->
    <section class="space-y-6">
      <h2 class="text-2xl font-bold text-white flex items-center gap-2">
        <Icon name="lucide:layers" class="text-indigo-400" />
        This Website
      </h2>
      <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-6">
        <a v-for="item in techStack" :key="item.name" :href="item.href" target="_blank" rel="noopener noreferrer"
          class="glass-panel glass-card-hover rounded-2xl p-6 border border-zinc-800/40 flex flex-col items-start gap-4">
          <div class="p-2 rounded-xl bg-zinc-900/60 border border-zinc-800 shrink-0">
            <Icon :name="item.icon" size="1.5rem" />
          </div>
          <div class="space-y-1">
            <h3 class="font-bold text-zinc-100 group-hover:text-indigo-400 transition-colors flex items-center gap-1">
              {{ item.name }}
              <Icon name="lucide:external-link" size="0.8rem" class="text-zinc-650" />
            </h3>
            <p class="text-zinc-400 text-xs leading-relaxed">
              {{ item.desc }}
            </p>
          </div>
        </a>
      </div>
    </section>

    <!-- Editor Setup Category -->
    <section class="space-y-6">
      <h2 class="text-2xl font-bold text-white flex items-center gap-2">
        <Icon name="lucide:monitor" class="text-indigo-400" />
        Editor & Terminal
      </h2>
      <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-6">
        <a v-for="item in editorSetup" :key="item.name" :href="item.href" target="_blank" rel="noopener noreferrer"
          class="glass-panel glass-card-hover rounded-2xl p-6 border border-zinc-800/40 flex flex-col items-start gap-4">
          <div class="p-2 rounded-xl bg-zinc-900/60 border border-zinc-800 text-indigo-400 shrink-0">
            <Icon :name="item.icon" size="1.5rem" />
          </div>
          <div class="space-y-1">
            <h3 class="font-bold text-zinc-100 group-hover:text-indigo-400 transition-colors flex items-center gap-1">
              {{ item.name }}
              <Icon name="lucide:external-link" size="0.8rem" class="text-zinc-655" />
            </h3>
            <p class="text-zinc-400 text-xs leading-relaxed">
              {{ item.desc }}
            </p>
          </div>
        </a>
      </div>
    </section>

    <!-- Editor Snapshot -->
    <section class="space-y-4 max-w-4xl mx-auto">
      <div class="relative group rounded-3xl overflow-hidden glass-panel p-2 shadow-2xl border border-zinc-800/40">
        <div class="absolute -inset-1 rounded-3xl bg-gradient-to-tr from-indigo-500 to-purple-600 opacity-20 blur-xl group-hover:opacity-30 transition-all duration-500"></div>
        <img src="~/assets/images/vscode_synthwave.png" alt="Visual Studio Code Synthwave 84 Theme" class="relative z-10 w-full rounded-2xl border border-zinc-800/50" />
      </div>
      <p class="text-center text-xs text-zinc-500 italic">Snapshot of my VS Code workstation running Synthwave '84</p>
    </section>
  </div>
</template>
