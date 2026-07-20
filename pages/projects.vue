<script setup>
const query = gql`
{
  viewer {
    repositories(first: 6, orderBy:{field:CREATED_AT,direction: DESC}) {
      totalCount
      nodes {
        id
        name
        createdAt
        description
        url
        forks {
          totalCount
        }
        watchers {
          totalCount
        }
        stargazers {
          totalCount
        }
      }
    }
  }
}
`

const mockProjects = [
  {
    id: 'mock-1',
    name: 'spring-boot-3-demo',
    description: 'A comprehensive collection of demos showcasing new features in Spring Boot 3 and Java 17+.',
    url: 'https://github.com/danvega/spring-boot-3-demo',
    stargazers: { totalCount: 142 },
    forks: { totalCount: 48 },
    watchers: { totalCount: 12 },
    language: 'Java'
  },
  {
    id: 'mock-2',
    name: 'nuxt-portfolio-template',
    description: 'A modern, premium portfolio template built with Nuxt 3, Tailwind CSS, and GraphQL.',
    url: 'https://github.com/danvega/nuxt-portfolio-template',
    stargazers: { totalCount: 89 },
    forks: { totalCount: 22 },
    watchers: { totalCount: 5 },
    language: 'Vue'
  },
  {
    id: 'mock-3',
    name: 'awesome-dev-advocacy',
    description: 'A curated list of resources, articles, and templates for Developer Advocates and Tech Evangelists.',
    url: 'https://github.com/danvega/awesome-dev-advocacy',
    stargazers: { totalCount: 210 },
    forks: { totalCount: 35 },
    watchers: { totalCount: 18 },
    language: 'Markdown'
  },
  {
    id: 'mock-4',
    name: 'graphql-java-api',
    description: 'An elegant GraphQL API implementation in Java using Spring GraphQL and Spring Data JPA.',
    url: 'https://github.com/danvega/graphql-java-api',
    stargazers: { totalCount: 64 },
    forks: { totalCount: 15 },
    watchers: { totalCount: 4 },
    language: 'Java'
  },
  {
    id: 'mock-5',
    name: 'vue3-composition-api-tips',
    description: 'A repository full of code snippets and guides on mastering Vue 3 Composition API best practices.',
    url: 'https://github.com/danvega/vue3-composition-api-tips',
    stargazers: { totalCount: 178 },
    forks: { totalCount: 42 },
    watchers: { totalCount: 9 },
    language: 'TypeScript'
  },
  {
    id: 'mock-6',
    name: 'nextjs-blog-cms',
    description: 'A head-to-head template combining Next.js with headless CMS tools and Tailwind CSS.',
    url: 'https://github.com/danvega/nextjs-blog-cms',
    stargazers: { totalCount: 95 },
    forks: { totalCount: 19 },
    watchers: { totalCount: 6 },
    language: 'TypeScript'
  }
]

const getLanguageByName = (name) => {
  const nameLower = name.toLowerCase();
  if (nameLower.includes('java') || nameLower.includes('spring')) return 'Java';
  if (nameLower.includes('vue') || nameLower.includes('nuxt')) return 'Vue';
  if (nameLower.includes('react') || nameLower.includes('next')) return 'TypeScript';
  if (nameLower.includes('css') || nameLower.includes('tailwind')) return 'CSS';
  return 'JavaScript';
};

const getLanguageColor = (lang) => {
  switch (lang) {
    case 'Java': return 'bg-orange-500/10 text-orange-400 border-orange-500/20';
    case 'Vue': return 'bg-emerald-500/10 text-emerald-400 border-emerald-500/20';
    case 'TypeScript': return 'bg-blue-500/10 text-blue-400 border-blue-500/20';
    case 'JavaScript': return 'bg-yellow-500/10 text-yellow-400 border-yellow-500/20';
    case 'CSS': return 'bg-pink-500/10 text-pink-400 border-pink-500/20';
    case 'Markdown': return 'bg-zinc-500/10 text-zinc-400 border-zinc-500/20';
    default: return 'bg-indigo-500/10 text-indigo-400 border-indigo-500/20';
  }
}

// Fetch query safely
const { data, error } = await useAsyncQuery(query).catch((err) => {
  console.warn("Apollo client failed to fetch data:", err);
  return { data: ref(null), error: ref(err) };
});

const isUsingMockData = computed(() => {
  return error.value || !data.value?.viewer?.repositories?.nodes;
});

const projects = computed(() => {
  if (isUsingMockData.value) {
    return mockProjects;
  }
  return data.value.viewer.repositories.nodes.map(node => ({
    id: node.id,
    name: node.name,
    description: node.description || 'No description provided.',
    url: node.url,
    stargazers: node.stargazers || { totalCount: 0 },
    forks: node.forks || { totalCount: 0 },
    watchers: node.watchers || { totalCount: 0 },
    language: getLanguageByName(node.name)
  }));
});

useSeoMeta({
  title: 'Projects | Dan Vega',
  description: 'Explore open source repositories and personal coding projects by Dan Vega.',
})
</script>

<template>
  <div class="space-y-12">
    <!-- Header -->
    <div class="space-y-4 text-left max-w-3xl">
      <h1 class="text-4xl font-extrabold tracking-tight text-white sm:text-5xl">
        Projects
      </h1>
      <p class="text-lg text-zinc-400 leading-relaxed">
        A selection of my public open-source projects hosted on GitHub. Feel free to explore, contribute, or star your favorites!
      </p>
    </div>

    <!-- Live API Status Banner -->
    <div v-if="isUsingMockData" class="glass-panel p-4 rounded-xl border-amber-500/20 bg-amber-500/5 text-amber-300 flex items-center gap-3 text-sm">
      <Icon name="lucide:alert-circle" size="1.25rem" class="shrink-0" />
      <div>
        <span class="font-semibold">Demo Mode:</span> Displaying mock repositories. Set a valid <code class="bg-amber-950/40 px-1 py-0.5 rounded border border-amber-500/20 text-xs">GITHUB_TOKEN</code> in your environment variables to fetch live repositories.
      </div>
    </div>

    <!-- Project Card Grid -->
    <section class="grid grid-cols-1 md:grid-cols-2 gap-8">
      <div v-for="project in projects" :key="project.id"
        class="glass-panel glass-card-hover rounded-2xl p-8 relative flex flex-col justify-between h-full border border-zinc-800/40">
        
        <div class="space-y-4">
          <!-- Top Bar: Title & Language Badge -->
          <div class="flex items-start justify-between gap-4">
            <a :href="project.url" target="_blank" rel="noopener noreferrer" class="group flex items-center gap-1">
              <h2 class="text-2xl font-bold text-zinc-100 group-hover:text-indigo-400 transition-colors line-clamp-1 leading-snug">
                {{ project.name }}
              </h2>
              <Icon name="lucide:external-link" size="1rem" class="text-zinc-500 group-hover:text-indigo-400 opacity-0 group-hover:opacity-100 transition-all" />
            </a>
            
            <span :class="[getLanguageColor(project.language), 'text-xs px-2.5 py-1 rounded-full border font-semibold shrink-0']">
              {{ project.language }}
            </span>
          </div>

          <!-- Description -->
          <p class="text-zinc-400 text-sm leading-relaxed line-clamp-3">
            {{ project.description }}
          </p>
        </div>

        <!-- Card Footer: Repo Stats -->
        <div class="mt-8 pt-4 border-t border-zinc-900/60 flex items-center gap-6 text-xs font-semibold text-zinc-400">
          <div class="flex items-center gap-1.5 hover:text-amber-400 transition-colors" title="Stars">
            <Icon name="lucide:star" size="1.05rem" class="text-zinc-500" />
            <span>{{ project.stargazers.totalCount }}</span>
          </div>
          
          <div class="flex items-center gap-1.5 hover:text-indigo-400 transition-colors" title="Forks">
            <Icon name="lucide:git-fork" size="1.05rem" class="text-zinc-500" />
            <span>{{ project.forks.totalCount }}</span>
          </div>
          
          <div class="flex items-center gap-1.5 hover:text-purple-400 transition-colors" title="Watchers">
            <Icon name="lucide:eye" size="1.05rem" class="text-zinc-500" />
            <span>{{ project.watchers.totalCount }}</span>
          </div>
        </div>

      </div>
    </section>
  </div>
</template>
